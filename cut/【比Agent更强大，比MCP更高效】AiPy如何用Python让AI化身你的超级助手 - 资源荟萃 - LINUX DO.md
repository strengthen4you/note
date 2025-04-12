# 【比Agent更强大，比MCP更高效】AiPy如何用Python让AI化身你的超级助手 - 资源荟萃 - LINUX DO
发现一个非常有意思的工具，今天给大家分享下：**AiPy（爱派）** 文末有具体安装方法

先给大家上效果，我的需求是

```null
从国家统计局查询最近10年中国的进出口数据，然后做成一张多维度图表
然后打开，并以图片格式保存到本地

```

[![](https://cdn.ldstatic.com/original/4X/8/a/9/8a91784e8881cef3d54df5680ef33d11de47085b.png)
](https://cdn.ldstatic.com/original/4X/8/a/9/8a91784e8881cef3d54df5680ef33d11de47085b.png)

有意思的中间出了个小插曲，它把自己整emo了一次

[![](https://cdn.ldstatic.com/original/4X/0/5/1/0510712d097fdc3d807b18394c78c1349473c00e.png)
](https://cdn.ldstatic.com/original/4X/0/5/1/0510712d097fdc3d807b18394c78c1349473c00e.png)

期间它自己打开了浏览器，然后又自动打开了统计局官网

[![](https://cdn.ldstatic.com/optimized/4X/9/a/d/9ada85b88587a2c6c2bfa0053d4db2b92f02c9fb_2_617x500.png)
](https://cdn.ldstatic.com/original/4X/9/a/d/9ada85b88587a2c6c2bfa0053d4db2b92f02c9fb.png)

自动标注目录结构，精准找到数据发布，然后从2014年开始依次自动查询。

中间页面跳的太快没来得截图

另一个有意思的是，在做数据分析的时候，它自己发现现在是2025年（开头那张图它还认为今年是2024年），然后回过头又重新找了今年的数据。

最终还给我在本地贴心的存了个数据图表的html页面，最终效果

[![](https://cdn.ldstatic.com/optimized/4X/7/2/f/72fe0dfa11f7ad905242add4c29411562a1d613c_2_690x345.png)
](https://cdn.ldstatic.com/original/4X/7/2/f/72fe0dfa11f7ad905242add4c29411562a1d613c.png)

[![](https://cdn.ldstatic.com/optimized/4X/8/a/0/8a0a995179795b31e9b3b1c50a0b04214ef0f55f_2_689x347.png)
](https://cdn.ldstatic.com/original/4X/8/a/0/8a0a995179795b31e9b3b1c50a0b04214ef0f55f.png)

[![](https://cdn.ldstatic.com/optimized/4X/4/4/8/448317f5d586c199ac6cd64705777528989e0712_2_689x342.png)
](https://cdn.ldstatic.com/original/4X/4/4/8/448317f5d586c199ac6cd64705777528989e0712.png)

全程总共用时10分钟左右（跟用哪个大模型也有关系）

省流版直接怼GitHub

* * *

所以，简单来说，**爱派**是基于Python为AI赋予了"双手"——不仅能理解你的需求，还能自动编写并执行Python代码来完成具体任务，解决 **如何让AI不只是思考，还能实际行动。** 

[![](https://cdn.ldstatic.com/optimized/4X/7/b/f/7bfd6e55640eb8105a40cb92e3d01bb085a64ca0_2_690x328.png)
](https://cdn.ldstatic.com/original/4X/7/b/f/7bfd6e55640eb8105a40cb92e3d01bb085a64ca0.png)

### [](#p-5092403-aipy-1)那AiPy为何如此与众不同？

[![](https://cdn.ldstatic.com/optimized/4X/b/e/b/bebdce1049590c182f5ff5bd301efc1229f691c5_2_690x315.jpeg)
](https://cdn.ldstatic.com/original/4X/b/e/b/bebdce1049590c182f5ff5bd301efc1229f691c5.jpeg "2025-04-12")

#### [](#p-5092403-h-2)传统大模型：只能对话，不能行动

*   擅长回答问题、生成内容
*   无法直接操作计算机、处理数据
*   面向问答

#### [](#p-5092403-agent-3)传统Agent系统：依赖大量特定工具

*   需要开发、安装和配置多个专用Agent
*   扩展性受限于可用Agent
*   通常需要云端部署，数据安全隐忧
*   Token消耗较高

#### [](#p-5092403-aipypythonagent-4)AiPy全新范式：Python就是最通用的Agent

*   直接利用Python的强大生态
*   实时编码和执行，无需预定义工具
*   本地处理敏感数据，保障隐私安全
*   更低的Token消耗成本
*   真正实现"AI Think & Do"

### [](#p-5092403-no-agents-code-is-agent-5)"No Agents, Code is Agent"的革命性理念

AiPy创造性地提出了一个大胆理念：**真正的通用AI Agent是NO Agents!**

传统思路是开发越来越多的专用Agent，但AiPy颠覆性地认为，这种做法反而限制了AI的能力发挥。

Python作为一种极其通用的编程语言，几乎可以实现任何计算任务、与任何系统交互。

因此，比起开发数百个专用Agent，不如让AI直接使用Python:

*   Python可以操作数据
*   Python可以控制计算机
*   Python可以访问网络
*   Python可以连接物联网设备
*   Python可以…几乎做任何事

亦即：**人类使用AI，AI使用Python，Python使用世界**。

### [](#p-5092403-aipy-6)AiPy的实际优势

#### [](#p-5092403-h-1-7)1\. 开源免费，成本可控

*   完全开源，代码托管在GitHub
*   用户只需负担LLM API的token费用
*   支持多种大模型，包括DeepSeek、Ollama等

#### [](#p-5092403-h-2-8)2\. 本地部署，数据安全

*   所有数据处理在本地完成
*   敏感信息不会离开你的设备
*   适合处理大型文件和保密数据

#### [](#p-5092403-h-3-9)3\. 高度灵活，无限可能

*   不受预定义工具限制
*   可调用各类API，包括私有/本地API
*   可处理几乎任何Python能完成的任务

#### [](#p-5092403-h-4-10)4\. 面向任务，而非面向代码

*   交付的是最终结果，而非中间代码
*   用户只需表达意图，无需关心实现细节
*   自我调试和改进能力

### [](#p-5092403-h-2-11)快速上手，2分钟上手

环境要求：thon 版本≥3.9

**Windows上手教程**

① 懒人版下载

[AFF](https://linux.do/tag/AFF) [https://wreabnvkfptcazgt.aqyun.org/downloads/aipy20250411.zip](https://wreabnvkfptcazgt.aqyun.org/downloads/aipy20250411.zip)

无需安装，自带运行环境，运行即可使用！运行解压包中的update.bat可升级到最新版。

② 安装python的

```null
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
pip config set global.trusted-host mirrors.aliyun.com
pip install --upgrade pip
pip install aipyapp

```

**macOS/Linux 上手教程**

macOS/Linux 系统自带 Python2，需要先升级至 Python3 后，即可使用 pip install aipyapp 一键安装

新建一个文件名为`aipython.toml` ,基础版格式配置：

```null
[llm.trustoken]
api_key = "your key"
base_url = "https://api.trustoken.ai/v1/"
model = "auto"
max_tokens = 16384
enable = true
default = true

```

首次配置必读：  
1、在配置aipython.toml前，请确保你已经安装好了aipy。  
2、首次使用aipy，可以直接在https:/api.trustoken.ai 申请一个免费key  
3、然后将申请到的key，替换aipython.toml中的“your key”,注意只替换双引号内的，替换后保存aipython.toml。  
4、然后把aipython.toml放到你的任意目录下，然后使用cmd/终端，切换到该目录，并在cmd命令中输入aipy，即可开始使用aipy  
5、更多高阶配置，可以访问 [AFF](https://linux.do/tag/AFF) [https://discuss.aipy.app/](https://discuss.aipy.app/) 了解。

* * *

这一圈操作下给我最大的感受：**不是通过增加更多专用工具来扩展AI能力，而是赋予AI直接利用通用编程语言的能力，这将极大拓展AI的应用边界。** 

现在倒是可以畅享下在不久的将来

AI将能够帮助普通用户完成各种复杂任务，无需编程知识

而开发者可以专注于更高层次的创新，而非重复开发各类Agent

那么，你觉得呢？ 欢迎讨论交流

原文![](https://cdn.linux.do/images/emoji/twemoji/link.png?v=14)
 [AFF](https://linux.do/tag/AFF) [https://mp.weixin.qq.com/s/s3\_KBV1tkSrSo39O\_njoEA](https://mp.weixin.qq.com/s/s3_KBV1tkSrSo39O_njoEA)

* * *

补充一个进阶版配置

把`txt`后缀换成 `toml`

[aipython.txt](https://linux.do/uploads/short-url/7cLGLYbTQizWkbOC1lAwJIrdUiv.txt) (8.8 KB)