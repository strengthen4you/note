# 免费部署容器对比，佬们来一起补充更新 - 文档共建 / 文档共建, Lv1 - LINUX DO
免费容器网站对比，比如vercel，replit，zeabur，cloudflare等，按是否需要信用卡，其他免费条件，免费用户可以使用哪些功能，支持哪些部署方式，支持的开发需要比如docker,go等维度分析对比。

1.  **Cloudflare**

*   免费：提供worker&pages免费服务，真神
*   需要信用卡：可能需要（取决于服务）
*   部署方式：主要提供CDN和边缘计算服务
*   开发技术：支持静态网站和通过Workers运行JavaScript
*   推荐理由：强大的CDN服务，提供边缘计算能力，适合静态网站加速和动态内容处理。

2.  **Vercel**

*   免费：是（Serverless，100G流量）
*   需要信用卡：否
*   部署方式：支持静态网站、Next.js等框架，不支持Docker
*   开发技术：支持多种前端技术栈
*   推荐理由：界面美观，操作简单直观，免费资源充足，适合前端项目快速部署。

3.  **Netlify** （与vercel类似，100GB流量+300分钟构建时间）

*   免费：是(主要部署前端，使用邮箱注册需要验证手机号；推荐使用GitHub+稍微干净的IP登录注册，即可无需验证手机号)
*   需要信用卡：否
*   部署方式：主要针对静态网站部署
*   开发技术：支持前端技术栈
*   推荐理由：静态网站部署服务的领导者，提供Edge Functions。

4.  **Render**

*   免费：是（有限制，需保活，一段时间不访问，会停机，有流量后会触发服务启动,老用户不会弹CC，新用户使用邮箱注册会弹CC）。您的免费实例将在不活动时关闭，这可能会使请求延迟 50 秒或更长时间。
*   需要信用卡：可能需要（取决于服务）
*   部署方式：支持多种服务，包括Docker
*   开发技术：支持多种编程语言和框架
*   推荐理由：功能丰富，提供750小时的免费服务时间。

5.  **Hugging Face**

*   免费：是（提供免费公共模型托管和基础计算资源，部分高级功能需付费）
*   需要信用卡：否（本地部署模型完全免费，需保活）
*   部署方式：支持Docker容器化部署、静态应用及API代理服务。
*   开发技术：支持Transformers库（Python）、Node.js等，兼容OpenAI API格式
*   推荐理由：全球最大开源AI社区，提供1000万美元免费共享GPU资源，适合AI模型开发与部署，支持国内网络优化方案。

6.  **Clawcloud**

*   免费：是（满180天GitHub可每月赠送5美元永久免费额度，最高可选4核8G内存配置）
*   需要信用卡：否（GitHub老账号注册即享，无需绑定）
*   部署方式：支持Docker容器化部署、一键部署WordPress/Alist等款应用
*   开发技术：支持PHP/Go/Java/Python等主流语言5，兼容阿里云生态
*   推荐理由：永久免费高配容器天花板（4核CPU+8G内存+10G带宽），亚洲节点访问友好，适合部署Alist/青龙面板/AI模型等低流量项目

7.  **Koyeb**

*   免费：是（有限制，需要保活，1个web应用，1个postgre数据库（0.25vCPU, 1G存储），不能绑自定义域, 按组织确定免费，目前可以建2个组织，每个组织可以建1个web应用，1个postgre数据库【待进一步确认】）
*   需要信用卡：Hobby计划不需要信用卡，Starter 0元计划需要信用卡验证1$
*   部署方式：支持Docker容器部署
*   开发技术：支持多种编程语言和Docker
*   推荐理由：简单易用，弹性扩展，适合容器化应用部署。

8.  **Zeabur**

*   免费：是(免费区域现在是空的，您只能部署免费试用区域的服务。所有位于免费试用区域的项目将在 24 小时后自动删除。)
*   需要信用卡：否
*   部署方式：支持多种编程语言和框架，支持Docker
*   开发技术：支持Docker, Python, Node.js等
*   推荐理由：支持支付宝，适合国内用户，提供CI/CD，支持前端、后端、数据库一站式部署。
*   [![](https://linux.do/uploads/default/optimized/4X/1/4/d/14dc989416e50003ab329e7719a102fec826d3d2_2_690x398.png)
    ](https://linux.do/uploads/default/original/4X/1/4/d/14dc989416e50003ab329e7719a102fec826d3d2.png)
    

9.  **Railway** （新用户已无免费额度&有GitHub活跃检测，不推荐使用）

*   免费：是（新用户已无免费额度，老用户只能部署数据库，不能部署其他服务。Tips: 如果你不是新用户，五刀用完了，别慌，点击右上角头像进入settings->General->拉到最下面Delete Account，对，这是注销解绑，然后再重新用github登录绑定，然后你会发现，又有五刀了）
*   需要信用卡：可能需要（取决于服务）
*   部署方式：支持多种部署方式，包括Docker
*   开发技术：支持多种编程语言和框架
*   推荐理由：支持一键部署，界面清晰，适合快速原型设计。
*   [![](https://linux.do/uploads/default/optimized/4X/8/b/c/8bc4d16121f91ae3e3c9294c94643b4895503b66_2_690x200.png)
    ](https://linux.do/uploads/default/original/4X/8/b/c/8bc4d16121f91ae3e3c9294c94643b4895503b66.png)
    

10.  **Replit** （3个APP限制，10个Agent Checkpoints）

*   免费：是（有限制，适合开发调试验证，需开浏览器存活）
*   需要信用卡：否
*   部署方式：支持多种编程语言的在线编辑器和运行环境
*   开发技术：支持多种编程语言
*   推荐理由：适合学习和小型项目，提供在线开发环境。
*   在线IDE类似平台：腾讯CNB，腾讯cloud studio(推荐)

\=帖子里支持docker的都有免费时间，用完就没了，hf 除了不能直接使用自己域名和慢点，更好点

总结的很好![](https://linux.do/images/emoji/twemoji/+1.png?v=14)

甲骨文 ![](https://linux.do/images/emoji/twemoji/melting_face.png?v=14)

这个是VPS了，玄学ABC ![](https://linux.do/images/emoji/twemoji/laughing.png?v=14)

Zeabur实际上就是收费了； Koyeb 我记得多少天之后也会不行了，具体忘记了抱歉；

至于Cloudflare听说可以期待一波，后面会有新惊喜。

另外，可以补充一下部署项目的数量。比如 render 只能白嫖一个。

cloudflare，huggingface真神，可以说正常使用完全无限制