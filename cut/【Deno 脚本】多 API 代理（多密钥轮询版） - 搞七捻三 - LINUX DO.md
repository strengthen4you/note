# 【Deno 脚本】多 API 代理（多密钥轮询版） - 搞七捻三 - LINUX DO
基于 [@ZXZX](https://linux.do/u/zxzx) 佬的[新多模型API安全代理（已修复gemini代理）](https://linux.do/t/topic/359495) 修改了下，支持了多Key轮询 ![](https://cdn.ldstatic.com/original/3X/2/e/2e09f3a3c7b27eacbabe9e9614b06b88d5b06343.png?v=14)

感谢 [@ZXZX](https://linux.do/u/zxzx) 佬、[@F-droid](https://linux.do/u/f-droid) 佬等大佬的提供的原始脚本 ![](https://cdn.ldstatic.com/original/3X/4/9/49b2eba636dba687d98c4254bb00c682194f3556.png?v=14)

**备注：如果号池体量比较大，请修改代码，改用KV存储 `${provider}Keys`**  
**备注：小脚本不适合高并发场景（keyIndex作为密钥索引、频繁读写 KV 、读取环境变量）**

**修复：2025-03-09 | 代理 Gemini 并启用轮询模式时，请求时仅将密钥作为 key 参数传入，也能通过鉴权**

* * *

[](#p-4420232-h-1)脚本代码
----------------------

点击展开```
import { serve } from "https://deno.land/std@0.178.0/http/server.ts";

const kv = await Deno.openKv();

// -------------------- 1. 自定义配置--------------------
// 路径映射
// 键名中斜杠后的部分（如`gemini`）将会作为后续变量 provider 的值，用以标记服务商
const apiMapping: Record<string, string> = {
  "/openai": "https://api.openai.com",
  "/claude": "https://api.anthropic.com",
  "/gemini": "https://generativelanguage.googleapis.com",
  "/xai": "https://api.x.ai",
  "/groq": "https://api.groq.com/openai",
  "/openrouter": "https://openrouter.ai/api",
  "/meta": "https://www.meta.ai/api",
  "/cohere": "https://api.cohere.ai",
  "/huggingface": "https://api-inference.huggingface.co",
  "/together": "https://api.together.xyz",
  "/novita": "https://api.novita.ai",
  "/portkey": "https://api.portkey.ai",
  "/fireworks": "https://api.fireworks.ai",
  "/cerebras": "https://api.cerebras.ai",
  "/discord": "https://discord.com/api",
  "/telegram": "https://api.telegram.org",
};

// 密钥轮询配置：是否对各 provider 启用密钥轮询
// 如果没有在这里配置，则默认过滤敏感请求头后直接转发请求
const rotationConfig: Record<string, boolean> = {
  gemini: true,
  groq: true,
};

// 鉴权请求头格式声明：请在此处声明不同 provider 的鉴权请求头格式
// 如果没有在这里声明，则默认使用 "Authorization: Bearer ${apiKey}"
const authHeaderMapping: Record<string, (apiKey: string) => [string, string]> = {
  gemini: (apiKey: string) => ["x-goog-api-key", apiKey],
  claude: (apiKey: string) => ["x-api-key", apiKey],
};

// -------------------- 2. 敏感请求头过滤 --------------------
const deniedHeaders = ["host", "referer", "cf-", "forward", "cdn"];
function isAllowedHeader(key: string): boolean {
  const lowerKey = key.toLowerCase();
  for (const deniedHeader of deniedHeaders) {
    if (lowerKey.includes(deniedHeader)) {
      return false;
    }
  }
  return true;
}

// -------------------- 3. parseTarget：尝试匹配 provider 并且提取路径 --------------------
function parseTarget(urlPath: string): { provider: string; targetUrl: string } {
  const splitIndex = urlPath.indexOf("/", 1);
  if (splitIndex === -1) {
    return { provider: "", targetUrl: "" };
  }
  const prefix = urlPath.substring(0, splitIndex);
  const provider = prefix.replace("/", "");
  const mappedBase = apiMapping[prefix];
  if (!mappedBase) {
    return { provider: "", targetUrl: "" };
  }
  const restPath = urlPath.substring(prefix.length);
  return {
    provider,
    targetUrl: mappedBase + restPath,
  };
}

// -------------------- 4. 处理密钥池与轮询索引 --------------------
async function getKeyPool(provider: string): Promise<string[]> {
  const envKeyName = `${provider}Keys`;
  const keyPoolStr = Deno.env.get(envKeyName);
  if (!keyPoolStr) return [];
  return keyPoolStr.split(",").map((k) => k.trim()).filter((k) => k.length > 0);
}

async function atomicIncrementRotationIndex(
  provider: string,
  length: number,
): Promise<number> {
  const key = ["keyIndex", provider];
  for (let attempt = 0; attempt < 5; attempt++) {
    const { value: oldIndex, versionstamp } = await kv.get<number>(key);
    const safeOldIndex = oldIndex ?? 0;
    const newIndex = (safeOldIndex + 1) % length;
    const ok = await kv.atomic()
      .check({ key, versionstamp })
      .set(key, newIndex)
      .commit();
    if (ok) {
      return safeOldIndex;
    }
  }
  throw new Error(`atomicIncrementRotationIndex: failed after multiple attempts`);
}

// -------------------- 5. 传入请求头鉴权 --------------------
function extractInboundAuthKey(
  request: Request,
  provider: string,
): string | undefined {
  const buildAuthHeader = authHeaderMapping[provider];
  if (buildAuthHeader) {
    const [customHeaderKey] = buildAuthHeader("");
    return request.headers.get(customHeaderKey) || undefined;
  } else {
    const incomingAuth = request.headers.get("Authorization");
    if (!incomingAuth || !incomingAuth.startsWith("Bearer ")) {
      return undefined;
    }
    return incomingAuth.substring("Bearer ".length).trim();
  }
}

function checkInboundAuth(request: Request, provider: string): boolean {
  const envAuthKey = Deno.env.get("authKey");
  if (!envAuthKey) {
    // 未在环境变量中配置 authKey 者无法执行鉴权流程，视作鉴权失败
    return false;
  }
  const inboundKey = extractInboundAuthKey(request, provider);
  if (inboundKey === envAuthKey) {
    return true;
  }
  // 当 Gemini 有关的请求无法通过 "x-goog-api-key" 头完成鉴权时，尝试通过 url 中的参数 key 鉴权
  if (provider === "gemini") {
    const url = new URL(request.url);
    const keyParam = url.searchParams.get("key");
    return keyParam === envAuthKey;
  }
  return false;
}

// -------------------- 6. 启动服务，处理请求 --------------------
serve(async (request: Request) => {
  const url = new URL(request.url);
  const pathname = url.pathname + url.search;

  // 特殊路由：根路径, /robots.txt
  if (pathname === "/" || pathname === "/index.html") {
    return new Response("Service is running!", {
      status: 200,
      headers: { "Content-Type": "text/html" },
    });
  }
  if (pathname === "/robots.txt") {
    return new Response("User-agent: *\nDisallow: /", {
      status: 200,
      headers: { "Content-Type": "text/plain" },
    });
  }

  // 解析目标地址，判断是否启用密钥轮询
  let { provider, targetUrl } = parseTarget(pathname);
  if (!targetUrl) {
    return new Response("无效路径: " + pathname, { status: 404 });
  }
  const rotationEnabled = rotationConfig[provider] ?? false;

  // 过滤敏感请求头
  const headers = new Headers();
  for (const [key, value] of request.headers.entries()) {
    if (isAllowedHeader(key)) {
      headers.set(key, value);
    }
  }

  // -------------------- 无需轮询者直接转发 --------------------
  if (!rotationEnabled) {
    try {
      return await fetch(targetUrl, {
        method: request.method,
        headers,
        body: request.body,
      });
    } catch (error) {
      const message = `转发模式： ${targetUrl}\n\n` +
                      `错误消息: ${error.message}\n\n` +
                      `堆栈跟踪:\n${error.stack ?? 'No stack trace'}`;
      return new Response(message, { status: 500 });
    }
  }

  // -------------------- 8. 需轮询者，鉴权后重新构造请求头与转发 --------------------
  if (!checkInboundAuth(request, provider)) {
    return new Response("轮询模式：脚本鉴权未通过", { status: 401 });
  }

  const keyPool = await getKeyPool(provider);
  if (keyPool.length === 0) {
    return new Response(`轮询模式：${provider} 缺少密钥池`, {
      status: 500,
    });
  }

  // 移除原有的鉴权请求头
  headers.delete("Authorization");
  headers.delete("x-api-key");
  headers.delete("x-goog-api-key");

  // 轮询模式代理 Gemini 时，删去 URL 中的参数 key
  // 经过测试，携带正确的 "x-goog-api-key"请求头，同时传入错误的 key 参数，API 仍然能够正常响应，所以此处的 if 语句，目前也不会引起问题
  if (provider === "gemini") {
    const targetUrlObj = new URL(targetUrl);
    targetUrlObj.searchParams.delete("key");
    targetUrl = targetUrlObj.toString();
  }

  // 读取并更新 KV 中的轮询索引，确定使用的密钥
  let currentIndex: number;
  try {
    currentIndex = await atomicIncrementRotationIndex(provider, keyPool.length);
  } catch (err) {
    return new Response(`轮询模式：密钥轮询索引更新失败: ${err.message}`, {
      status: 500,
    });
  }
  const apiKey = keyPool[currentIndex];

  // 根据 authHeaderMapping 确定目标格式，构造新的鉴权请求头
  const buildAuthHeader = authHeaderMapping[provider];
  let authHeaderKey = "Authorization";
  let authHeaderValue = `Bearer ${apiKey}`;
  if (buildAuthHeader) {
    [authHeaderKey, authHeaderValue] = buildAuthHeader(apiKey);
  }
  headers.set(authHeaderKey, authHeaderValue);

  // 发起请求
  try {
    return await fetch(targetUrl, {
      method: request.method,
      headers,
      body: request.body,
    });
  } catch (error) {
    const message = `轮询模式 - 请求失败： ${targetUrl}\n\n` +
                    `错误消息: ${error.message}\n\n` +
                    `堆栈跟踪:\n${error.stack ?? 'No stack trace'}`;
    return new Response(message, { status: 500 });
  }
}); 
``` 

* * *

[](#p-4420232-h-2)配置步骤
----------------------

### [](#p-4420232-h-1-3)1\. 自定义配置

*   `apiMapping`: 代理路径映射表
    
    *   可以自由添加和删除的路径映射
    *   通过 **字段名**（即服务商标记，后称 `provider`），映射到指定的 `baseURL`
*   `rotationConfig`: 密钥轮询配置
    
    *   在 **启用多密钥轮询** 时，相应 `provider` 字段的键值需要配置为 `true`
*   `authHeaderMapping`: 服务商鉴权请求头格式映射表
    
    *   在 **启用多密钥轮询** 时，请求头不是用 `Authorization: Bearer ${apiKey}` 鉴权的 api 需要设置（比如 Gemini, Claude）

### [](#p-4420232-h-2-4)2\. 配置环境变量

*   **`authKey`: 鉴权密钥**  
    （你想要在 One/New/Neo-API 渠道设置中、 Cherry Studio 模型服务设置中填入的密钥）
    
*   **`xxxKeys`: 密钥池文本变量**  
    （要求用 **半角逗号**`,` 分隔，不必用引号包裹）  
    （如果要密钥轮询，就需要在环境变量里配置 `${provider}Keys`，比如 `geminiKeys`）
    

### [](#p-4420232-h-5)**示例说明**

*   像上方的代码，**我需要 Gemini 和 Groq 的密钥轮询**，所以我这样配置：
    
    *   根据 `apiMapping` 中 Gemini 和 Groq 的映射方式，确定服务商标记 **gemini** 和 **groq**，它们在接下来设置 `rotationConfig` 和 `authHeaderMapping` 的过程中会被用到，并**加粗显示**。  
        \*.deno.dev/**gemini**/\* → **[https://generativelanguage.googleapis.com/](https://generativelanguage.googleapis.com/)**\*  
        \*.deno.dev/**groq**/\* → **[https://api.groq.com/openai/](https://api.groq.com/openai/)**\*
        
    *   在 `rotationConfig` 中设置密钥轮询  
        `gemini: true,`  
        `groq: true,`
        
    *   因为 Gemini API 使用 `x-goog-api-key: ${apiKey}` 鉴权，而不是 `Authorization: Bearer ${apiKey}` ，所以需要在 `authHeaderMapping` 中声明鉴权请求头的格式：  
        **gemini**: (apiKey: string) => \[“**x-goog-api-key**”, apiKey\],
        
    *   Groq 兼容 OpenAI 格式，无需在 `authHeaderMapping` 中作声明
        
    *   在环境变量中配置 鉴权密钥 和 密钥池
        
        *   `geminiKeys` 的值，设置为 `AIcrazyThu,AIvMeFifty`
        *   `groqKeys` 的值，设置为 `gsk_crazyThu,gsk_vMeFifty`

[](#p-4420232-h-6)脚本工作流程
------------------------

![](https://quickchart.io/graphviz?graph=digraph%20G%20%7Brankdir%3DTB%3Bnode%20%5Bshape%3Dbox%5D%3Bstart%20%5Bshape%3Dellipse%2Clabel%3D%22%E5%BC%80%E5%A7%8B%22%5D%3Bstep1%20%5Blabel%3D%221.%20%E8%AF%B7%E6%B1%82%E5%A4%84%E7%90%86%20%26%20%E8%B7%AF%E7%94%B1%E5%88%86%E5%8F%91%22%5D%3Bstep2%20%5Blabel%3D%222.%20%E8%AF%B7%E6%B1%82%E5%A4%B4%E8%BF%87%E6%BB%A4%22%5D%3Bstep3%20%5Bshape%3Ddiamond%2Clabel%3D%22%E5%90%AF%E7%94%A8%E8%BD%AE%E8%AF%A2%EF%BC%9F%22%5D%3Bstep4%20%5Blabel%3D%224.%20%E5%AE%A2%E6%88%B7%E7%AB%AF%E9%89%B4%E6%9D%83%22%5D%3Bstep5%20%5Blabel%3D%225.%20%E5%AF%86%E9%92%A5%E6%B1%A0%E9%AA%8C%E8%AF%81%22%5D%3Bstep6%20%5Blabel%3D%226.%20%E5%AF%86%E9%92%A5%E8%BD%AE%E8%AF%A2%20%26%20%E9%89%B4%E6%9D%83%E5%A4%B4%E6%9E%84%E9%80%A0%22%5D%3Bstep7%20%5Blabel%3D%227.%20%E8%AF%B7%E6%B1%82%E8%BD%AC%E5%8F%91%20%26%20%E5%93%8D%E5%BA%94%22%5D%3Berror401%20%5Bshape%3Dellipse%2Clabel%3D%22%E8%BF%94%E5%9B%9E%20401%20Unauthorized%22%2Ccolor%3Dred%5D%3Berror500%20%5Bshape%3Dellipse%2Clabel%3D%22%E8%BF%94%E5%9B%9E%20500%20Internal%20Error%22%2Ccolor%3Dred%5D%3Bfetch_error%20%5Bshape%3Dellipse%2Clabel%3D%22%E8%BF%94%E5%9B%9E%20500%20%E9%94%99%E8%AF%AF%22%2Ccolor%3Dred%5D%3Bend%20%5Bshape%3Dellipse%2Clabel%3D%22%E7%BB%93%E6%9D%9F%22%2Ccolor%3Dgreen%5D%3Bstart-%3Estep1%3Bstep1-%3Estep2%3Bstep2-%3Estep3%3Bstep3-%3Estep4%20%5Blabel%3D%22%E6%98%AF%22%5D%3Bstep3-%3Estep7%20%5Blabel%3D%22%E5%90%A6%22%5D%3Bstep4-%3Eerror401%20%5Blabel%3D%22%E5%A4%B1%E8%B4%A5%22%5D%3Bstep4-%3Estep5%20%5Blabel%3D%22%E6%88%90%E5%8A%9F%22%5D%3Bstep5-%3Eerror500%20%5Blabel%3D%22%E6%97%A0%E6%95%88%22%5D%3Bstep5-%3Estep6%20%5Blabel%3D%22%E6%9C%89%E6%95%88%22%5D%3Bstep6-%3Estep7%3Bstep7-%3Efetch_error%20%5Blabel%3D%22%E9%94%99%E8%AF%AF%22%5D%3Bstep7-%3Eend%20%5Blabel%3D%22%E6%88%90%E5%8A%9F%22%5D%3B%7D)

service is running，不过用cherry 试gemini没有成功。authKey 和 geminiKey都设置了。

这个问题的原因应该是 Cherry Studio 在获取模型的时候使用的是

*   GET `${baseURL}/v1/models?key=${apiKey}`
*   GET `${baseURL}/v1beta/models?key=${apiKey}`

也就是说: Cherry 获取模型的时候没有传入 “x-goog-api-key” 这个请求头  
对脚本来说，相当于没有提供密钥，所以返回了 401 错误

但是实际聊天时, Cherry 传入了 “x-goog-api-key” 这个请求头  
所以**获取模型失败，但手动添加模型可以成功聊天**

* * *

[](#p-4429553-h-1)解决方案（可直接回到顶楼使用调整后的代码）
---------------------------------------

1.  修改鉴权函数 **checkInboundAuth** ，在 x-goog-api-key 请求头缺失或校验失败的情况下，回退使用 URL 中的参数 key 鉴权。

```null
function checkInboundAuth(request: Request, provider: string): boolean {
  const envAuthKey = Deno.env.get("authKey");
  if (!envAuthKey) {
    
    return false;
  }
  const inboundKey = extractInboundAuthKey(request, provider);
  if (inboundKey === envAuthKey) {
    return true;
  }
  
  if (provider === "gemini") {
    const url = new URL(request.url);
    const keyParam = url.searchParams.get("key");
    return keyParam === envAuthKey;
  }
  return false;
}

```

2.  （可选）在通过鉴权之后从 URL 中删除 key 参数  
    在**第 8 部分**的**第一个 if 语句**以下的位置，加入这段代码

```null
  
  
  if (provider === "gemini") {
    const targetUrlObj = new URL(targetUrl);
    targetUrlObj.searchParams.delete("key");
    targetUrl = targetUrlObj.toString();
  }

```

支持！昨天刚发现这个脚本部署完，今天又有佬优化了！

[![](https://cdn.ldstatic.com/optimized/4X/3/3/8/338384ee4d49f7b037a0f5040e8a7deb15523b7f_2_690x208.png)
](https://cdn.ldstatic.com/original/4X/3/3/8/338384ee4d49f7b037a0f5040e8a7deb15523b7f.png "image")

我这里没成功，也许我设置有误

这个错误是脚本而不是 API 返回的，说明 Deno 部署的脚本没有收到正确的 authKey ，可以先检查一下环境变量里的 **authKey** 是不是配置错了（比如输错了，或者用引号包裹、带上了其他字符）。

首先，多谢大佬的分享。我想将这个配合我的lobechat使用，请问这个 \[多密钥轮询版\] ，我可以在那里放置我的密钥，我想放3个密钥，请问可以放到那里，谢谢请指教一下。  

[![](https://cdn.ldstatic.com/optimized/4X/6/2/0/62076757d5c2828f994240c0ba84e7f0ffc8d84b_2_371x500.png)
](https://cdn.ldstatic.com/original/4X/6/2/0/62076757d5c2828f994240c0ba84e7f0ffc8d84b.png "image")

需要先在 rotationConfig 里面开启轮询  
添加 ${provider}: true

然后再点击编辑器上方的按钮，在弹出的面板里边，配置两个相应的环境变量噢

*   ${provider}Keys （“密钥池”）
*   authKey （“自定义密码”）

[![](https://cdn.ldstatic.com/optimized/4X/7/9/b/79b898510a1b53e883fc5692dd5f016effb88864_2_465x500.jpeg)
](https://cdn.ldstatic.com/original/4X/7/9/b/79b898510a1b53e883fc5692dd5f016effb88864.jpeg "editor")

比如用的是 gemini 的 key  
那么根据 apiMapping 就可以确定 provider  
是已经写好的 gemini  
所以就是 gemini:true 和环境变量 geminiKeys, authKey

[![](https://cdn.ldstatic.com/optimized/4X/8/9/d/89d59dd2c9d6b3444aab7c6d7baade9da09a2ee7_2_375x500.jpeg)
](https://cdn.ldstatic.com/original/4X/8/9/d/89d59dd2c9d6b3444aab7c6d7baade9da09a2ee7.jpeg "env")

多谢大佬的回覆，我现在试试。 ![](https://linux.do/images/emoji/twemoji/grinning_face.png?v=14)

谢谢大佬的帮忙，我设置好了，可是那个"论询"的功能不成功，请问我再这里输入两组api？要有分隔和用甚么格式输入？谢谢请指教。谢谢帮忙。  

[![](https://cdn.ldstatic.com/optimized/4X/5/4/0/5409c4f407a63a8ffe8d83b1033a9809eaa0c14d_2_690x414.png)
](https://cdn.ldstatic.com/original/4X/5/4/0/5409c4f407a63a8ffe8d83b1033a9809eaa0c14d.png "image")

比如你的三个Key是 AI123 ，AI456 和 AI789  
就是将 geminiKeys 的值设置成：  
AI123,AI456,AI789

authKey 是你用来保护你密钥池子（也就是号池）的密码，随心设置就好了

所以假设你只需要给 gemini 堆号池的话，只需要确保编辑器里的 rotationConfig 包含  
gemini: true ，然后按照上面的要求在图中 Value 的位置输入中间夹逗号的密钥就好了

多谢大佬的指导，现已设立好了。 非常多谢您的帮忙。 ![](https://linux.do/images/emoji/twemoji/grinning_face.png?v=14)

已经在本地服务器上部署好了，可是感觉用了这个api的速度（就是以前几乎是输入问题，大概1-2秒就开始出答案了），用了这个轮询器后大概要等个8-10秒，就好像是哪里卡住了，但本地机器上，deno域名是做了加速的，秒开，google ai stiduio那个域名也是秒开，不知道是哪里的问题

我用了这个一段时间，暂时都很稳定。  
如果第一个号爆了，重新生成就会自己切换另一个api key。  
我比搞过直接连上去，跟用这个暂时看不到速度上的分别。

我用了这个一段时间，暂时都很稳定。  
如果第一个号爆了，重新生成就会自己切换另一个api key。  
我比搞过直接连上去，跟用这个暂时看不到速度上的分别。