# 写给小白的2$/月 美国原生家宽ip解决方案 - 开发调优 / 开发调优, Lv1 - LINUX DO
本文是写给**小白**的美国家宽ip便宜解决方案，价格大约2.05$/月，步骤非常详细  
**不探讨家宽的真伪和各种属性**，只是提供一个优于万人骑垃圾ip机场的可参考的方案。  
主贴无任何站外链接，aff链接放在二楼，愿意的话可以点击一下，供大家使用。  
ip效果（ping0图一乐），具体效果要看你自己淘到的ip怎么样  

[![](https://linux.do/uploads/default/original/4X/5/1/5/515b343598fbf3f0f9ca1ba7a6efe3bd58f147e8.png)
](https://linux.do/uploads/default/original/4X/5/1/5/515b343598fbf3f0f9ca1ba7a6efe3bd58f147e8.png "image")

**小白**跟着操作，无需任何技术含量。

**1.线路鸡的选择**

本文使用Nube的线路，在中国线路优化方案里，这个是相当不错的选择  
注意：**nube是10$起充的**，不想充的私信我开节点，我账号上有钱，直接转我就行，  
反正是小时计费，用多少算多少  

[![](https://linux.do/uploads/default/optimized/4X/f/8/e/f8e7f773ffa1203c36ae5b3da8aaf1291f61f7a4_2_323x500.png)
](https://linux.do/uploads/default/original/4X/f/8/e/f8e7f773ffa1203c36ae5b3da8aaf1291f61f7a4.png "image")

  

[![](https://linux.do/uploads/default/original/4X/8/f/2/8f2274c99777b7480a999170d90601c339903677.png)
](https://linux.do/uploads/default/original/4X/8/f/2/8f2274c99777b7480a999170d90601c339903677.png "image")

按照流量20g算(对节点要求高的场景如gpt/注册一个月肯定用不了20g)  
线路鸡的费用大概0.9733+0.0187\*20 =1.3473$  
点击下单，回到主页

[![](https://linux.do/uploads/default/optimized/4X/9/7/3/9736d9a6737bddd01e4fce0e84c6fd43e40ca613_2_690x196.png)
](https://linux.do/uploads/default/original/4X/9/7/3/9736d9a6737bddd01e4fce0e84c6fd43e40ca613.png "image")

选个Debian11或者ubuntu22，这里随便，以ubuntu22为例子

[![](https://linux.do/uploads/default/optimized/4X/9/8/2/9827baa37065182132f104e53dc133ab199881db_2_690x380.png)
](https://linux.do/uploads/default/original/4X/9/8/2/9827baa37065182132f104e53dc133ab199881db.png "image")

点击安装等交付，交付后进入管理界面

[![](https://linux.do/uploads/default/optimized/4X/f/7/5/f75a92917163c7df7dccedfb2599db2254ed4f20_2_690x402.png)
](https://linux.do/uploads/default/original/4X/f/7/5/f75a92917163c7df7dccedfb2599db2254ed4f20.png "image")

注意左下角SSH内容(本文发出时，主机已删除，无所谓打码)  
安装XSHELL/finalshell等工具，安装过程可以自行搜索(猜猜本站为啥叫**LINUX DO**) ![](https://linux.do/images/emoji/twemoji/zany_face.png?v=14)
  
用SSH工具（本文用finalshell为例）连接后，看到以下页面，证明登录成功

[![](https://linux.do/uploads/default/optimized/4X/6/6/2/66202b59dbc7083ec62581956fd788cc143edad1_2_690x376.jpeg)
](https://linux.do/uploads/default/original/4X/6/6/2/66202b59dbc7083ec62581956fd788cc143edad1.jpeg "image")

好了，下面不用管控制台了，挂着即可，如果自动退出了就按照上述流程再来一次进行登录

**2.落地ip的选择**  
这里使用Webshare，具体怎么购买操作可看这位大佬的文章，价格8.5$~12$/年

但是这篇文章看到“配置clash分流和链式代理”就不用看了，这不是**小白**的内容  

[![](https://linux.do/uploads/default/optimized/4X/2/f/3/2f361cf9e1a3f9bed615067c26b679bf83d14c36_2_690x432.png)
](https://linux.do/uploads/default/original/4X/2/f/3/2f361cf9e1a3f9bed615067c26b679bf83d14c36.png "image")

个人最近测试，这四个ip段还不错

```null
38.154.5.x
69.30.77.x
69.30.74.x
207.228.8.x

```

购买完毕并且淘到了喜欢的ip后，你会看到这个页面(这个ip我在用，所以打码了)  

[![](https://linux.do/uploads/default/optimized/4X/c/a/d/cadd1b5408656a1341eb3a5c8592954ca3dfc78f_2_690x149.png)
](https://linux.do/uploads/default/original/4X/c/a/d/cadd1b5408656a1341eb3a5c8592954ca3dfc78f.png "image")

现在落地ip也准备好了，下面回到刚刚的控制台

**3.代理准备**  
直接采用vless+reality的协议  
输入

```null
bash <(curl -L https://raw.githubusercontent.com/wzwys9/my_abc/main/install.sh)

```

看到这个页面  

[![](https://linux.do/uploads/default/optimized/4X/4/1/b/41bbee1867fcf56de470c92aa182c14ec98633e7_2_655x499.jpeg)
](https://linux.do/uploads/default/original/4X/4/1/b/41bbee1867fcf56de470c92aa182c14ec98633e7.jpeg "image")

输入`1`等待执行，随后看到下方页面

[![](https://linux.do/uploads/default/optimized/4X/8/f/f/8ff0123ab7366f338eda18f325fd78d888cf7820_2_690x92.png)
](https://linux.do/uploads/default/original/4X/8/f/f/8ff0123ab7366f338eda18f325fd78d888cf7820.png "image")

输入`4`，然后一直回车默认，直到看到这个

[![](https://linux.do/uploads/default/optimized/4X/a/e/f/aefe25f9bc05fdca840fe5b367a7a4c148c6f32d_2_690x376.jpeg)
](https://linux.do/uploads/default/original/4X/a/e/f/aefe25f9bc05fdca840fe5b367a7a4c148c6f32d.jpeg "image")

输入`y`，然后回到之前的Webshare购买页面，依次输入ip/端口/用户名/密码后

[![](https://linux.do/uploads/default/original/4X/8/e/7/8e71e6ea5c345653b6e2a53491d5e16c89008121.png)
](https://linux.do/uploads/default/original/4X/8/e/7/8e71e6ea5c345653b6e2a53491d5e16c89008121.png "image")

一直回车默认选择到底，直到看到下面页面

[![](https://linux.do/uploads/default/optimized/4X/9/d/c/9dc0bba270e4ce899375833d5449364989c7f946_2_690x431.jpeg)
](https://linux.do/uploads/default/original/4X/9/d/c/9dc0bba270e4ce899375833d5449364989c7f946.jpeg "image")

一直往上滑动页面，直到看到这个

[![](https://linux.do/uploads/default/optimized/4X/a/7/6/a76bc7579b5fd69d722daeaeaaf1e7e41198c9ec_2_690x73.png)
](https://linux.do/uploads/default/original/4X/a/7/6/a76bc7579b5fd69d722daeaeaaf1e7e41198c9ec.png "image")

复制下来

```null
vless://01838d17-2bd2-391b-b74d-0ad62ed91497@65.75.222.103:7999?flow=xtls-rprx-vision&encryption=none&type=tcp&security=reality&sni=learn.microsoft.com&fp=random&pbk=6yatTLPq5qnb6VDRO5j0qmMRhjilYlrzGLtuAXUW4mk&sid=77dcaa7e785e3980&

```

BBR开启等配置自行搜索  
在站内或者google搜索订阅转换，复制粘贴链接，生成订阅链接  

[![](https://linux.do/uploads/default/optimized/4X/9/5/5/95592d4e79cfa76330d0d67889b32f1b5895ec07_2_650x500.jpeg)
](https://linux.do/uploads/default/original/4X/9/5/5/95592d4e79cfa76330d0d67889b32f1b5895ec07.jpeg "image")

打开代理软件导入(本文以clash为例)，看到可以连通

[![](https://linux.do/uploads/default/original/4X/1/e/e/1ee938785193866ba0d70270f70841d1d8456594.png)
](https://linux.do/uploads/default/original/4X/1/e/e/1ee938785193866ba0d70270f70841d1d8456594.png "image")

使用，打开where is my ip看看，发现已经变成落地ip ![](https://linux.do/images/emoji/twemoji/clinking_beer_mugs.png?v=14)

价格上计算，1.3473+8.5/12 =2.05$/月 流量20g为基准。多用多扣，少用少扣。  
对于小白如果想要再搭建一个不走Webshare的普通节点(走webshare延时会高，而且网速一般)，只要在上面XRAY面板选择是否开启socks5代理选择n即可获得，这样一个代理会走优质ip，一个会走普通ip，对于个人自建纯自用来说，美国节点就完全搞掂了！

题外话:  
1.关于线路鸡的选择，这个nube是性价比比较不错的方案，当然有其他更好的线路鸡也可以用，但是如果你都有线路鸡了，恐怕和小白不沾边hh。  
2.关于落地ip的探讨：Webshare是真家宽吗？肯定不算，但是质量一定比万人骑高的多，至于想要质量更好的家宽，那就不是2$/月能解决的了hh，不过还有一个深层次的问题：检测代理难道只看你的ip纯净度吗？所以说，家宽这个东西见仁见智，测试都是图一乐，真正还要看体验。  
3.关于协议的选择：写给小白的，越简单越好，越稳越好，其他协议自行搜索解决。

**下面不是写给小白的内容：**   
关于我推荐的nube服务器的线路方案测评(晚高峰测的，供参考)，这个价格我能找到的好鸡了

MJJ不骗MJJ，骗人mjj

```
--------------------- A Bench Script By spiritlhl ----------------------
                   测评频道: https://t.me/vps_reviews                    
VPS融合怪版本：2025.02.12
Shell项目地址：https://github.com/spiritLHLS/ecs
Go项目地址：https://github.com/oneclickvirt/ecs
-------------IP质量检测--基于oneclickvirt/securityCheck使用-------------
数据仅作参考，不代表100%准确，如果和实际情况不一致请手动查询多个数据库比对
以下为各数据库编号，输出结果后将自带数据库来源对应的编号
ipinfo数据库  [0] | scamalytics数据库 [1] | virustotal数据库   [2] | abuseipdb数据库   [3] | ip2location数据库    [4]
ip-api数据库  [5] | ipwhois数据库     [6] | ipregistry数据库   [7] | ipdata数据库      [8] | db-ip数据库          [9]
ipapiis数据库 [A] | ipapicom数据库    [B] | bigdatacloud数据库 [C] | cheervision数据库 [D] | ipqualityscore数据库 [E]
IPV4:
安全得分:
声誉(越高越好): 0 [2] 
信任得分(越高越好): 19 [8] 
VPN得分(越低越好): 44 [8] 
代理得分(越低越好): 100 [8] 
社区投票-无害: 0 [2] 
社区投票-恶意: 0 [2] 
威胁得分(越低越好): 100 [8]
欺诈得分(越低越好): 65 [E] 50 [1]
滥用得分(越低越好): 0 [3] 
ASN滥用得分(越低越好): 0.0013 (Low) [A] 
公司滥用得分(越低越好): 0.0039 (Low) [A] 
威胁级别: low [9 B] 
黑名单记录统计:(有多少黑名单网站有记录):
无害记录数: 0 [2]  恶意记录数: 0 [2]  可疑记录数: 0 [2]  无记录数: 94 [2]  
安全信息:
使用类型: corporate [9] hosting [0 7 A] business [8] DataCenter/WebHosting/Transit [3] unknown [C]
公司类型: isp [A] hosting [0 7]
是否云提供商: Yes [7 D] 
是否数据中心: Yes [0 1] No [5 6 8 A C]
是否移动设备: No [5 A C] Yes [E]
是否代理: Yes [E] No [0 1 4 5 6 7 8 9 A B C D]
是否VPN: Yes [E] No [0 1 6 7 A C D]
是否TorExit: No [1 7 D] 
是否Tor出口: No [1 7 D] 
是否网络爬虫: No [9 A B E] 
是否匿名: No [1 6 7 8 D] 
是否攻击者: No [7 8 D] 
是否滥用者: No [7 8 A C D E] 
是否威胁: No [7 8 C D] 
是否中继: No [0 7 8 C D] 
是否Bogon: No [7 8 A C D] 
是否机器人: No [E] 
DNS-黑名单: 313(Total_Check) 0(Clean) 7(Blacklisted) 20(Other) 
Google搜索可行性：NO
-------------邮件端口检测--基于oneclickvirt/portchecker开源-------------
Platform  SMTP  SMTPS POP3  POP3S IMAP  IMAPS
LocalPort ✔     ✔     ✔     ✔     ✔     ✔    
QQ        ✔     ✔     ✔     ✘     ✔     ✘    
163       ✔     ✔     ✔     ✘     ✔     ✘    
Sohu      ✔     ✔     ✔     ✘     ✔     ✘    
Yandex    ✔     ✔     ✔     ✘     ✔     ✘    
Gmail     ✔     ✔     ✘     ✘     ✘     ✘    
Outlook   ✔     ✘     ✔     ✘     ✔     ✘    
Office365 ✔     ✘     ✔     ✘     ✔     ✘    
Yahoo     ✔     ✔     ✘     ✘     ✘     ✘    
MailCOM   ✔     ✔     ✔     ✘     ✔     ✘    
MailRU    ✔     ✔     ✘     ✘     ✔     ✘    
AOL       ✔     ✔     ✘     ✘     ✘     ✘    
GMX       ✔     ✘     ✔     ✘     ✔     ✘    
Sina      ✔     ✔     ✔     ✘     ✔     ✘    
Apple     ✘     ✘     ✘     ✘     ✘     ✘    
FastMail  ✘     ✔     ✘     ✘     ✘     ✘    
ProtonMail✘     ✘     ✘     ✘     ✘     ✘    
MXRoute   ✔     ✘     ✔     ✘     ✔     ✘    
Namecrane ✔     ✔     ✔     ✘     ✔     ✘    
XYAMail   ✘     ✘     ✘     ✘     ✘     ✘    
ZohoMail  ✘     ✔     ✘     ✘     ✘     ✘    
Inbox_eu  ✔     ✔     ✔     ✘     ✘     ✘    
Free_fr   ✘     ✔     ✔     ✘     ✔     ✘    
----------------三网回程--基于oneclickvirt/backtrace开源----------------
北京电信 219.141.140.10  移动CMIN2  [精品线路] 
北京联通 202.106.195.68  联通4837   [普通线路] 
北京移动 221.179.155.161 移动CMIN2  [精品线路] 
上海电信 202.96.209.133  移动CMIN2  [精品线路] 
上海联通 210.22.97.1     联通4837   [普通线路] 
上海移动 211.136.112.200 移动CMIN2  [精品线路] 
广州电信 58.60.188.222   移动CMIN2  [精品线路] 
广州联通 210.21.196.6    联通4837   [普通线路] 
广州移动 120.196.165.24  移动CMIN2  [精品线路] 
成都电信 61.139.2.69     移动CMIN2  [精品线路] 
成都联通 119.6.6.6       联通4837   [普通线路] 
成都移动 211.137.96.205  移动CMIN2  [精品线路] 
准确线路自行查看详细路由，本测试结果仅作参考
同一目标地址多个线路时，可能检测已越过汇聚层，除了第一个线路外，后续信息可能无效
---------------------回程路由--感谢fscarmen开源及PR---------------------
依次测试电信/联通/移动经过的地区及线路，核心程序来自nexttrace，请知悉!
广州电信 58.60.188.222
0.37 ms         AS138997 美国 加利福尼亚 圣何塞 eons.cloud
0.63 ms         * [Nube-BB] 美国 加利福尼亚 圣何塞
0.33 ms         * [Nube-BB] 美国 加利福尼亚 圣何塞
13.15 ms        AS138997 [Nube-BB] 美国 加利福尼亚 圣何塞 eons.cloud
141.08 ms       AS58807 [CMIN2-NET] 美国 加利福尼亚 洛杉矶 cmi.chinamobile.com 移动
138.13 ms       AS58807 [CMIN2-NET] 中国 上海 cmi.chinamobile.com 移动
140.34 ms       AS9808 [CMNET] 中国 上海 chinamobileltd.com 移动
139.80 ms       AS9808 [CMNET] 中国 上海 chinamobileltd.com 移动
140.82 ms       AS9808 [CMNET] 中国 上海 chinamobileltd.com 移动
170.19 ms       AS9808 [CMNET] 中国 广东 广州 chinamobileltd.com 移动
171.34 ms       AS9808 [CMNET] 中国 广东 广州 chinamobileltd.com 移动
168.48 ms       AS4134 中国 广东 深圳 福田区 www.chinatelecom.com.cn 电信
广州联通 210.21.196.6
0.48 ms         AS138997 美国 加利福尼亚 圣何塞 eons.cloud
0.91 ms         * [Nube-BB] 美国 加利福尼亚 圣何塞
0.39 ms         * [Nube-BB] 美国 加利福尼亚 圣何塞
0.82 ms         * RFC1918
2.80 ms         AS4837 [CU169-BACKBONE] 美国 加利福尼亚 圣何塞 chinaunicom.cn 联通
160.54 ms       AS4837 [CU169-BACKBONE] 中国 上海 chinaunicom.cn 联通
161.23 ms       AS4837 [CU169-BACKBONE] 中国 上海 chinaunicom.cn 联通
184.62 ms       AS17816 [APNIC-AP] 中国 广东 深圳 chinaunicom.cn 联通
211.27 ms       AS17623 [APNIC-AP] 中国 广东 深圳 chinaunicom.cn 联通
182.67 ms       AS17623 中国 广东 深圳 宝安区 chinaunicom.cn 联通
广州移动 120.196.165.24
0.55 ms         AS138997 美国 加利福尼亚 圣何塞 eons.cloud
0.72 ms         * [Nube-BB] 美国 加利福尼亚 圣何塞
0.38 ms         * [Nube-BB] 美国 加利福尼亚 圣何塞
12.72 ms        AS138997 [Nube-BB] 美国 加利福尼亚 圣何塞 eons.cloud
138.33 ms       AS58807 [CMIN2-NET] 美国 加利福尼亚 洛杉矶 cmi.chinamobile.com 移动
138.21 ms       AS58807 [CMIN2-NET] 中国 上海 cmi.chinamobile.com 移动
138.28 ms       AS9808 [CMNET] 中国 上海 chinamobileltd.com 移动
138.29 ms       AS9808 [CMNET] 中国 上海 chinamobileltd.com 移动
139.37 ms       AS9808 [CMNET] 中国 上海 chinamobileltd.com
162.26 ms       AS9808 [CMNET] 中国 北京 chinamobileltd.com 移动
163.70 ms       AS9808 [CMNET] 中国 北京 chinamobileltd.com 移动
165.27 ms       AS56040 [APNIC-AP] 中国 广东 深圳 gd.10086.cn 移动
--------------------自动更新测速节点列表--本脚本原创--------------------
位置             上传速度        下载速度        延迟     丢包率
Speedtest.net    7681.17 Mbps    5759.54 Mbps    0.55     0.5%
洛杉矶           942.30 Mbps     717.24 Mbps     13.17    0.0%
日本东京         2151.37 Mbps    6339.13 Mbps    108.65   NULL
联通上海5G       16.66 Mbps      6183.65 Mbps    123.00   0.0%
联通Beijing      607.17 Mbps     2690.08 Mbps    162.56   0.0%
电信浙江         574.44 Mbps     2660.36 Mbps    158.31   NULL
电信浙江         532.84 Mbps     902.18 Mbps     146.43   NULL
移动Fujian       450.84 Mbps     478.72 Mbps     172.26   NULL
------------------------------------------------------------------------
 总共花费      : 5 分 24 秒
 时间          : Sun Mar  9 09:45:24 UTC 2025
------------------------------------------------------------------------ 
```

```
--------------------- A Bench Script By spiritlhl ----------------------
                   测评频道: https://t.me/vps_reviews                    
VPS融合怪版本：2025.02.12
Shell项目地址：https://github.com/spiritLHLS/ecs
Go项目地址：https://github.com/oneclickvirt/ecs
------------流媒体解锁--基于oneclickvirt/CommonMediaTests开源-----------
以下测试的解锁地区是准确的，但是不是完整解锁的判断可能有误，这方面仅作参考使用
----------------Netflix-----------------
[IPV4]
您的出口IP完整解锁Netflix，支持非自制剧的观看
NF所识别的IP地域信息：美国
[IPV6]
您的网络可能没有正常配置IPv6，或者没有IPv6网络接入
----------------Youtube-----------------
[IPV4]
连接方式: Google Global CacheCDN (ISP Cooperation)
ISP运营商: FCIXUS
视频缓存节点地域: SJC(SJC1)
[IPV6]
Youtube在您的出口IP所在的国家不提供服务
---------------DisneyPlus---------------
[IPV4]
当前IPv4出口所在地区即将开通DisneyPlus
[IPV6]
DisneyPlus在您的出口IP所在的国家不提供服务
解锁Netflix，Youtube，DisneyPlus上面和下面进行比较，不同之处自行判断
----------------流媒体解锁--感谢RegionRestrictionCheck开源--------------
 以下为IPV4网络测试，若无IPV4网络则无输出
============[ Multination ]============
 Dazn:                                  Yes (Region: US)
 Disney+:                               Yes (Region: US)
 Netflix:                               Yes (Region: US)
 YouTube Premium:                       Yes (Region: US)
 Amazon Prime Video:                    Yes (Region: US)
 TVBAnywhere+:                          Yes
 Spotify Registration:                  No
 OneTrust Region:                       US [California]
 iQyi Oversea Region:                   US
 Bing Region:                           US (Risky)
 Apple Region:                          US
 YouTube CDN:                           [FCIXUS] in [San Jose, CA]
 Netflix Preferred CDN:                 San Jose, CA
 ChatGPT:                               Yes
 Google Gemini:                         Yes (Region: USA)
 Claude:                                Yes
 Wikipedia Editability:                 No
 Google Play Store:                     United States 
 Google Search CAPTCHA Free:            Yes
 Steam Currency:                        USD
 ---Forum---
 Reddit:                                Yes
=======================================
 以下为IPV6网络测试，若无IPV6网络则无输出
---------------TikTok解锁--感谢lmc999的源脚本及fscarmen PR--------------
 Tiktok Region:         【US】
------------------------------------------------------------------------
 总共花费      : 25 秒
 时间          : Sun Mar  9 09:52:00 UTC 2025
------------------------------------------------------------------------ 
```

参考文献：

第一次写相关文章，操作不当技术问题还请大佬指出 ![](https://linux.do/images/emoji/twemoji/smiling_face_with_three_hearts.png?v=14)