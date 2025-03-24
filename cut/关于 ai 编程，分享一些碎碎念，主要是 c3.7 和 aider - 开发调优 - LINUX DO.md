# 关于 ai 编程，分享一些碎碎念，主要是 c3.7 和 aider - 开发调优 - LINUX DO
[

❤️ 再忍不住，也不要做这种事啊 ❤️

](https://linux.do/t/topic/482293)

[关于 ai 编程，分享一些碎碎念，主要是 c3.7 和 aider](/t/topic/490383)
====================================================

[开发调优](/c/develop/4)

[人工智能](/tag/人工智能),[作品集](/tag/作品集)

您已选择 **0** 个帖子。

全选

取消选择

​

[3月 13 日](/t/topic/490383/1 "跳到第一个帖子")

1 / 50

3月 13 日

[1 天 前](/t/topic/490383/52)

热门回复 ​

[![](https://linux.do/user_avatar/linux.do/leeorz/48/509067_2.png)
](/u/leeorz)

[近战法师](/u/leeorz)[leeorz](/u/leeorz)指导顾问 ![](https://linux.do/images/emoji/twemoji/speech_balloon.png?v=14) 

1

[11 天](/t/topic/490383?u=zhanpeng "发布日期")

从[gifcapture：纯前端实现的gif录制程序，即用即走![](https://linux.do/images/emoji/twemoji/tada.png?v=14)
](https://linux.do/t/topic/489993)继续讨论：

也算是从零开始用ai写完了一个小项目，分享一下用ai编程的过程，脑子比较乱，就当水贴了。

ai 能作为生产力工具，这应该是共识了吧？如何实践？那就写一个小项目吧。

项目选型不能太复杂，也不能太简单，因为毕竟要实践怎么能让 ai 融入日常的写代码任务中，所以项目的技术栈选型要符合以下几点：

*   整个项目的基础要是我熟悉的领域，否则就变成纯学习了。
*   技术栈不能完全小众，不能是 ai 完全不知道的东西。毕竟大模型上下文长度在那放着呢。
*   技术选型要有我完全不了解的组件，因为我需要一个 ai 知道但是我不知道场景，实践一下在这个场景下 ai 如何辅助人
*   所用的技术最近要有更新，以便测试如何让ai处理他的训练数据没有的内容

所以最后就选择做一个录制 gif 的小工具，技术栈是：vite ,react, shadcn, tailwindcss v4 ，konva，gif.js

我不熟悉的领域是 canvas，视频流，gif，其中完全不了解的技术组件是 konva 。

最近有更新的是 tailwindcss v4，配置方式完全不一样了，附带着 shadcn 的配置也不一样了

[](#p-4524297-h-1)工具选择
----------------------

从去年底就一直在折腾这些东西，cursor, cline，aider。

先说cursor，好东西，贵。这玩意从他一开始放出来就下载体验了，当时还没 c3.5 ，我嫌弃他是单独的 ide，我原本折腾了好久的vscode又得换掉，有点抵触，最后 c3.5 出来以后它彻底出圈。最大的缺点是白嫖太折腾，生产力工具不稳定，比吃屎还难受，而且订阅了以后限制还是很大，500次一月根本不够用，所以pass

再说cline，这玩意和 roo code 其实差不多，合并一起唠。  
我真是无力吐槽，[用量图](https://linux.do/t/topic/444145/132) ，这个帖子是我用cline配置mcp时候的 token 用量图，输入 150w token，输出 3w token，这是人干事？我甚至都还没开始写代码！它的实现思路就是把 prompt 和 用户提问，还有项目源码一股脑往 llm 那里塞，直到把 LLM 上下文塞爆，然后再重新对话，垃圾玩意滚粗。

再说 aider，这是我目前用下来体验最好，强推。

*   命令行工具，你可以在vscode单独开一个终端，挂在那里就行，无缝集成
*   所以用 jb 写 java 应该也可以挂一个aider在终端，但我没试过
*   使用repo map做项目结构给 LLM，这点完爆 cline，[可以看这里](https://aider.chat/docs/repomap.html#using-a-repo-map-to-provide-context)
*   architect 模式，推理模型专注规划，非推理模型专注修改，LLM 本身也是越具体的小任务就做的越好
*   指哪改哪，也就是说，除非你明确的添加文件为可修改，否则不瞎改
*   深度集成 git ，~我从来没写过这么规范的 commit message~
*   它把它自己的文档做了arg，不会的直接 /help 问就好了
*   跟 copliot 无冲突，偶尔一眼能看到的错误就用 copilot 的补全改一下，不用去 aider 里面对话了。

[](#p-4524297-llm-2)LLm选择
-------------------------

c3.7 毋庸置疑，次一级选择是r1+v3， aider 的 architect 模式中 r1+v3 也可用，我大概10%的代码是用 r1+v3 写的，剩下的都是 c3.7。现在回想，如果非前端， r1+v3的组合应该也可以满足，但是可能需要自己小修小改

[](#p-4524297-h-3)过程体验
----------------------

c3.7 真是牛逼，在aider 的 architect 模式下，80%的任务一次过。剩下那20%的任务，现在回想起来，是我自己犯懒，完全不想思考了。当人犯懒，丢给LLM一个模糊任务，不能指望它把任务做的完全符合你心意，对吧？特别是在一个稍微有点规模的项目里面。除非你对任务没有什么要求，就想看模型自由发挥。

当人完全没思路的时候，就用 /ask 模式聊，聊各种解决方案，聊完了就用 /code 让他实现。因为是深度集成了 git ，所以随便改，不合适回滚就是了。当清晰的知道解决思路，就用 /architect 直接写。

整个项目写了大概两个多星期，每天一两小时。konva 还是不会，但我知道了它的概念，大致的用法，你要让我手写，那没辙，我不了解具体的函数，就只知道它有那个功能函数，连函数名都不知道。

[](#p-4524297-h-4)总结
--------------------

*   有 ai 了以后，学习是更加必要的，但变了，广度比深度重要，除非你是搞前沿研究的。
*   实践变得更简单了，不需要扣每一个技术细节。
*   技术基础比技术框架更重要，前端娱乐圈那一堆狗屎了解下就好，脏活让LLM干

以及最后，真的会有 AGI 吗？ ![](https://linux.do/images/emoji/twemoji/melting_face.png?v=14)

[rules.zip](/uploads/short-url/v1Mo3spm2aDlIdraJ2TQEsqVoSs.zip) (2.7 KB)

  

1 个回复

![](https://linux.do/images/emoji/twemoji/heart.png?v=14)

heart

![](https://linux.do/images/emoji/twemoji/+1.png?v=14)

+1

![](https://linux.do/images/emoji/twemoji/laughing.png?v=14)

laughing

![](https://linux.do/images/emoji/twemoji/open_mouth.png?v=14)

open\_mouth

63

​ ​ 回复

*   [aider 配置说明](https://linux.do/t/topic/492021)
*   [【![](https://linux.do/images/emoji/twemoji/school.png?v=14)
    共同学习拔高】佬友们一人能留下自己任务效率最高的AI使用方法吗？一起看一下佬友们都是怎么用AI提升真正的工作or生活效率的？](https://linux.do/t/topic/489843/17)

1.4k 浏览量 115 赞 5 链接 29 用户

 [![](https://linux.do/user_avatar/linux.do/leeorz/48/509067_2.png)
  15](/u/leeorz "leeorz") 

 [![](https://linux.do/user_avatar/linux.do/_maoyu/48/406482_2.png)
  4](/u/_maoyu "_maoyu") 

 [![](https://linux.do/user_avatar/linux.do/whk/48/369996_2.png)
  2](/u/whk "whk") 

 [![](https://linux.do/user_avatar/linux.do/zbakajaa/48/516734_2.png)
  2](/u/Zbakajaa "Zbakajaa") 

 [![](https://linux.do/user_avatar/linux.do/laurdawn/48/373564_2.png)
  2](/u/laurdawn "laurdawn") 

阅读时间 4 分钟

热门回复

总结

上次访问

[![](https://linux.do/user_avatar/linux.do/s_line/48/95112_2.png)
](/u/s_line)

[s\_line](/u/s_line)一元复始

[11 天](/t/topic/490383/2?u=zhanpeng "发布日期")

![](https://linux.do/user_avatar/linux.do/leeorz/48/509067_2.png)
 近战法师:

> aider

提示词可以分享一下吗

  

1 个回复

10

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/cimix/48/196794_2.png)
](/u/Cimix)

[Cimix](/u/Cimix)指导顾问

[11 天](/t/topic/490383/3?u=zhanpeng "发布日期")

让AI来写代码主要是省事，经常有些需要查找并改写的，让AI来就是几秒钟的事情

我最常用的就是改样式。

刚回复完，又扣了$20，又有快速额度了，真好

  

7

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/leeorz/48/509067_2.png)
](/u/leeorz)

[近战法师](/u/leeorz)[leeorz](/u/leeorz)指导顾问 ![](https://linux.do/images/emoji/twemoji/speech_balloon.png?v=14) 

 ![](https://linux.do/user_avatar/linux.do/s_line/24/95112_2.png)
 s\_line

[11 天](/t/topic/490383/4?u=zhanpeng "发布日期")

我把 rules 文件上传了，这都是 ai 写的

  

4

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/wjxiz1992/48/454109_2.png)
](/u/wjxiz1992)

[wjxiz1992](/u/wjxiz1992)

[11 天](/t/topic/490383/5?u=zhanpeng "发布日期")

分享：  
目前在尝试 代码里纯写prompt和胶水，发送给 LLM，让LLM 来生成代码 并且跑。

  

3

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/handsome/48/477777_2.png)
](/u/handsome)

[大帅哥](/u/handsome)[handsome](/u/handsome)种子用户 ![](https://linux.do/images/emoji/twemoji/rage.png?v=14) 

[11 天](/t/topic/490383/6?u=zhanpeng "发布日期")

会的，会有的

  

4

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/microsoft/48/2980_2.png)
](/u/Microsoft)

[Microsoft](/u/Microsoft)蛇来运转 ![](https://linux.do/images/emoji/twemoji/underage.png?v=14) 

[11 天](/t/topic/490383/7?u=zhanpeng "发布日期")

aider是不是两年没更新了？

  

1 个回复

1

​ ​ 回复

[![](https://linux.do/letter_avatar_proxy/v4/letter/t/cc9497/48.png)
](/u/TeQIng)

[TeQIng](/u/TeQIng)一元复始

[11 天](/t/topic/490383/8?u=zhanpeng "发布日期")

佬的c3.7 是什么渠道呀

  

2 个回复

2

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/leeorz/48/509067_2.png)
](/u/leeorz)

[近战法师](/u/leeorz)[leeorz](/u/leeorz)指导顾问 ![](https://linux.do/images/emoji/twemoji/speech_balloon.png?v=14) 

 ![](https://linux.do/letter_avatar_proxy/v4/letter/t/cc9497/24.png)
 TeQIng

[11 天](/t/topic/490383/9?u=zhanpeng "发布日期")

openrouter

  

1

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/leeorz/48/509067_2.png)
](/u/leeorz)

[近战法师](/u/leeorz)[leeorz](/u/leeorz)指导顾问 ![](https://linux.do/images/emoji/twemoji/speech_balloon.png?v=14) 

 ![](https://linux.do/user_avatar/linux.do/microsoft/24/2980_2.png)
 Microsoft

[11 天](/t/topic/490383/10?u=zhanpeng "发布日期")

怎么会呢，十小时前还有提交的。

这个项目组没什么宣传的，默默的好用

没有X账号，只有一个discord频道

  

3

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/_maoyu/48/406482_2.png)
](/u/_maoyu)

[\_maoyu](/u/_maoyu)蛇来运转 ![](https://linux.do/images/emoji/twemoji/clown_face.png?v=14) 

[11 天](/t/topic/490383/11?u=zhanpeng "发布日期")

cline消耗的token真是巨量，无力吐槽，我也想尝试下aider，但是感觉没cline好上手，不知道消耗token的量相比起来怎么样？ 另外，它支持MCP吗？

  

1 个回复

1

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/leeorz/48/509067_2.png)
](/u/leeorz)

[近战法师](/u/leeorz)[leeorz](/u/leeorz)指导顾问 ![](https://linux.do/images/emoji/twemoji/speech_balloon.png?v=14) 

 ![](https://linux.do/user_avatar/linux.do/_maoyu/24/406482_2.png)
 \_maoyu

[11 天](/t/topic/490383/12?u=zhanpeng "发布日期")

token 消耗好多了，就配置是纯文本配置，也还好，看看明天水一贴 aider 的配置的。

配完了很好上手

  

1 个回复

1

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/_maoyu/48/406482_2.png)
](/u/_maoyu)

[\_maoyu](/u/_maoyu)蛇来运转 ![](https://linux.do/images/emoji/twemoji/clown_face.png?v=14) 

 ![](https://linux.do/user_avatar/linux.do/leeorz/24/509067_2.png)
 近战法师

[11 天](/t/topic/490383/13?u=zhanpeng "发布日期")

aider支持MCP吗？

  

1 个回复

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/leeorz/48/509067_2.png)
](/u/leeorz)

[近战法师](/u/leeorz)[leeorz](/u/leeorz)指导顾问 ![](https://linux.do/images/emoji/twemoji/speech_balloon.png?v=14) 

 ![](https://linux.do/user_avatar/linux.do/_maoyu/24/406482_2.png)
 \_maoyu

[11 天](/t/topic/490383/14?u=zhanpeng "发布日期")

目前不支持

  

1 个回复

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/_maoyu/48/406482_2.png)
](/u/_maoyu)

[\_maoyu](/u/_maoyu)蛇来运转 ![](https://linux.do/images/emoji/twemoji/clown_face.png?v=14) 

 ![](https://linux.do/user_avatar/linux.do/leeorz/24/509067_2.png)
 近战法师

[11 天](/t/topic/490383/15?u=zhanpeng "发布日期")

那它完成代码任务的能力应该不如cline吧？

  

1 个回复

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/leeorz/48/509067_2.png)
](/u/leeorz)

[近战法师](/u/leeorz)[leeorz](/u/leeorz)指导顾问 ![](https://linux.do/images/emoji/twemoji/speech_balloon.png?v=14) 

 ![](https://linux.do/user_avatar/linux.do/_maoyu/24/406482_2.png)
 \_maoyu

[11 天](/t/topic/490383/16?u=zhanpeng "发布日期")

不清楚你什么意思，我用 cline 最难受的两点，一是 token 消耗，二是太容易失控乱改代码。

aider 这软件他有一个记录，有多少代码量是用 aider 自身写的，目前来看达到 80% 了，我觉得可以说明问题

  

1 个回复

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/_maoyu/48/406482_2.png)
](/u/_maoyu)

[\_maoyu](/u/_maoyu)蛇来运转 ![](https://linux.do/images/emoji/twemoji/clown_face.png?v=14) 

 ![](https://linux.do/user_avatar/linux.do/leeorz/24/509067_2.png)
 近战法师

[11 天](/t/topic/490383/17?u=zhanpeng "发布日期")

我想表达的是：同样的任务如果分别让cline和aider来完成的话，哪个的完成度会更出色一些， 因为cline可以使用MCP服务，所以我潜意识觉得cline完成的会更好些，不知道实际情况如何？

  

1 个回复

1

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/leeorz/48/509067_2.png)
](/u/leeorz)

[近战法师](/u/leeorz)[leeorz](/u/leeorz)指导顾问 ![](https://linux.do/images/emoji/twemoji/speech_balloon.png?v=14) 

 ![](https://linux.do/user_avatar/linux.do/_maoyu/24/406482_2.png)
 \_maoyu

[11 天](/t/topic/490383/18?u=zhanpeng "发布日期")

这得看任务规模还有模型自身能力吧？

mcp 是有很大想象空间，但我觉得这是在扩展 llm 能力边界，而不是解决问题的好坏

  

1

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/laurdawn/48/373564_2.png)
](/u/laurdawn)

[laurdawn](/u/laurdawn)一元复始

[11 天](/t/topic/490383/19?u=zhanpeng "发布日期")

aider怎么使用其他模型，比如gemini，文档只有apikey的说明，感觉入门太麻烦了

  

1 个回复

1

​ ​ 回复

[![](https://linux.do/user_avatar/linux.do/leeorz/48/509067_2.png)
](/u/leeorz)

[近战法师](/u/leeorz)[leeorz](/u/leeorz)指导顾问 ![](https://linux.do/images/emoji/twemoji/speech_balloon.png?v=14) 

 ![](https://linux.do/user_avatar/linux.do/laurdawn/24/373564_2.png)
 laurdawn

[11 天](/t/topic/490383/20?u=zhanpeng "发布日期")

是有点麻烦，他要配模型提供商前缀，根据前缀决定 api 格式，明天再水一贴算了

  

2 个回复

1

​ ​ 回复