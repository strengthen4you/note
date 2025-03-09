# Trae2API - 说明文档
项目介绍
----

Trae2API 是一个将 Trae API 转换为 OpenAI API 格式的服务，仅用于技术交流学习，不可用于任何商业行为！

声明：本项目未进行任何逆向、破解，仅提供基于明文HTTP API的包装服务。

### 功能特点

*   支持获取模型列表
*   支持多轮对话
*   支持流式输出
*   支持 Docker 部署

### 不会支持

*   代理访问，请部署在非国内的其他亚洲区域服务器
*   多账号轮询永远不会支持，虽然很简单

环境变量获取指南
--------

要使用 Trae2API最新版本，您需要获取以下环境变量。请按照对应平台的指南操作：

方式一：

执行以下脚本一键获取需要的环境变量值（作者:[linuxdo-Serendipity](https://linux.do/u/im594/summary)）：

curl -fsSL https://gist.githubusercontent.com/IM594/b0bbcdc3eb6a5e849f5e306246781a48/raw/get\_trae\_tokens.sh | bash

方式二：

参考Windows平台查找指定文件获取环境变量

脚本获取（作者:[linuxdo-keung](https://linux.do/u/keung/summary)）:

Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass

.\\get\_trae\_tokens.ps1

查询获取:

5.  安装 `everything` 工具
6.  搜索 `storge.json` 文件获取 RefreshToken,、UserID
7.  搜索 `main.log` 文件获取 ClientID
8.  搜索 `ai_1_stdout.log` 文件获取 AppID
9.  开启抓包软件 `在Trae上，上传一个图片，抓包软件查看上传地址`获取文件地址相关环境变量

您可以使用以下随机生成的 Token 作为 AUTH\_TOKEN：

aHofIQnkg0WKgyvWq5LGKOmpAMyejbWT

必需的环境变量
-------

Trae API 应用 ID，可从 ai\_1\_stdout.log 文件中获取

OAuth Client ID，可从 main.log 文件中获取

OAuth Refresh Token，可从 storge.json 文件中获取

User ID，可从 main.log 文件中获取

API 访问鉴权 Token，可自定义设置

建议使用数字+字母生成的字符串确保安全性，不要包含特殊字符

可选的环境变量
-------

获取模型、对话、获取文件上传Token的基本路径（如果你是亚洲区域，可以忽略此变量）

默认值：https://trae-api-sg.mchost.guru

刷新RefreshToken和Token的基本路径（如果你是亚洲区域，可以忽略此变量）

默认值：https://api-sg-central.trae.ai

获取上传文件ID的基础路径（如果你是亚洲区域，可以忽略此变量）

默认值：https://imagex-ap-singapore-1.bytevcloudapi.com

上传文件的基础路径（如果你是亚洲区域，可以忽略此变量）

默认值：https://tos-sg16-share.vodupload.com

API 使用示例
--------

GET http://localhost:17080/v1/models
Authorization: Bearer your\_auth\_token

curl http://localhost:17080/v1/models -H "Authorization: Bearer your\_auth\_token"

已复制!

POST http://localhost:17080/v1/chat/completions
Authorization: Bearer your\_auth\_token
Content-Type: application/json

{
  "model": "gpt-4o",
  "messages": \[
    {
      "role": "user",
      "content": "你好"
    }
  \],
  "stream": false
}

curl http://localhost:17080/v1/chat/completions \\ -H "Authorization: Bearer your\_auth\_token" \\ -H "Content-Type: application/json" \\ -d '{"model":"gpt-4o","messages":\[{"role":"user","content":"你好"}\],"stream":false}'

已复制!

POST http://localhost:17080/v1/chat/completions
Authorization: Bearer your\_auth\_token
Content-Type: application/json

{
  "model": "gpt-4o",
  "messages": \[
    {
      "role": "user",
      "content": "你好"
    }
  \],
  "stream": true
}

curl http://localhost:17080/v1/chat/completions \\ -H "Authorization: Bearer your\_auth\_token" \\ -H "Content-Type: application/json" \\ -d '{"model":"gpt-4o","messages":\[{"role":"user","content":"你好"}\],"stream":true}'

已复制!

常见问题解决方案
--------

不可以，此项目如果出现在Linux.do区域外的公网网站，则该项目会即刻停止更新并私有化镜像，交流需求可以加底部tg群。

Trae2api会使用本地的refreshToken来刷新Token，而refreshToken使用一次之后立即失效，会导致Trae本身记录的refreshToken失效无法刷新Token，如果你有Trae本身的使用需求，建议放弃使用本项目，或者在虚拟机或其他电脑中额外开启一个Trea用来提供2api服务。

目前已知refreshToken可持续刷新，理论字节不调整，可以持续使用。

当前配置的refreshToken失效了，请退出Trae的账号，重新登录，然后获取最新的refreshToken填入环境变量中,获取之后就不需要再打开Trae了。

Trae在不同的区域调用的是不同的接口地址，目前已知有sg（新加坡）和us（美国）两个不同的地址，默认使用sg的接口，你可以更换地址相关的环境变量以使用指定的接口地址。

尝试过，效果不是很好，遂放弃，刚好也防止号商拿去逆向。