# Hysteria2节点添加端口跳跃功能 - 开发调优 / 开发调优, Lv1 - LINUX DO
因本人使用的代理工具为Surge和Clash（分别用于苹果设备和Windows设备），因此在挑选协议时，Hysteria2居然成为了唯一的通用的选择【Surge不支持Vless，Clash不支持Snell v4】。虽然有佬友提出这个协议在不久后会被精准检测到，但目前来说我还能将就用一下。

之前写过一篇手动搭建Hysteria2节点的帖子。[【搭建教程】一步一步教你自建Hysteria2节点 - 开发调优 / 开发调优, Lv1 - LINUX DO](https://linux.do/t/topic/159235/4)

当时并没有讲述如何添加端口跳跃的功能（因为没有也能正常使用）。随着这个协议的普及，我觉得还是开启这个功能更好，能够有效避免运营商对UDP的QoS限制。

那么什么是端口跳跃呢？在 Hysteria2 中，端口跳跃是一种对抗流量识别和阻断的技术，它通过动态变换端口来隐藏流量特征。

> 官方文档介绍：[端口跳跃 - Hysteria 2](https://v2.hysteria.network/zh/docs/advanced/Port-Hopping/)
> 
> 中国用户有时报告运营商会阻断或限速 UDP 连接。不过，这些限制往往仅限单个端口。端口跳跃可用作此情况的解决方法。

下面正式进入配置教程，**以下教程作为续篇，请在之前的教程完成后接续使用**。

在服务器端，你只需要转发相应的端口范围即可。

[](#p-2099300-h-1-3)1.端口转发
--------------------------

Hysteria服务端并不能同时监听多个端口，因此不能在服务器端使用上面的格式作为监听地址。**建议配合 iptables 或 nftables 的 DNAT 将端口转发到服务器的监听端口。** 

### [](#p-2099300-h-11-4)**1.1查看网卡名称**

```null
ip a

```

[![](https://linux.do/uploads/default/original/3X/8/a/8a1f768c4297f9e35eb701a5e09a5a2e39c8eaee.png)
](https://linux.do/uploads/default/original/3X/8/a/8a1f768c4297f9e35eb701a5e09a5a2e39c8eaee.png "image")

我这里用的是亚马逊的LightSail做的演示，因此网卡的名称为ens5，一般默认的其实是eth0。

### [](#p-2099300-h-12-iptables-5)**1.2检查 iptables 命令是否可用**

```null
iptables --version

```

![](https://linux.do/uploads/default/original/3X/6/2/62ddbb94e45360f165592637d1e1deed481a0419.png)

> 如果未安装，安装 iptables
> 
> `sudo apt updatesudo apt install iptables`

### [](#p-2099300-h-13-iptables-6)**1.3检查 iptables 服务是否运行**

```null
sudo systemctl status iptables

```

[![](https://linux.do/uploads/default/original/3X/9/6/96645aee87ef55a4a86af40c9461c3fcbfbfde99.png)
](https://linux.do/uploads/default/original/3X/9/6/96645aee87ef55a4a86af40c9461c3fcbfbfde99.png "image")

### [](#p-2099300-h-14ipv4-7)**1.4配置IPv4端口转发**

```null
iptables -t nat -A PREROUTING -i eth0 -p udp --dport 30000:50000 -j REDIRECT --to-ports 443

```

### [](#p-2099300-h-15ipv6-8)**1.5配置IPv6端口转发**

```null
ip6tables -t nat -A PREROUTING -i eth0 -p udp --dport 30000:50000 -j REDIRECT --to-ports 443

```

### [](#p-2099300-h-16-9)**1.6查看是否设置成功**

```null
sudo iptables -t nat -L PREROUTING -v -n --line-numbers
sudo ip6tables -t nat -L PREROUTING -v -n --line-numbers

```

[![](https://linux.do/uploads/default/original/3X/d/d/dd5aae5a134e7cd0efca279dca4e7a8edd161ef7.png)
](https://linux.do/uploads/default/original/3X/d/d/dd5aae5a134e7cd0efca279dca4e7a8edd161ef7.png "image")

![](https://linux.do/uploads/default/original/3X/2/8/2894ec2469341d21ce7fb68431cb66334867395b.png)

### [](#p-2099300-h-17iptables-10)**1.7重启iptables命令**

```null
systemctl restart iptables.service

```

### [](#p-2099300-h-18iptables-11)**1.8iptables持久化**

iptables 的规则在机器重启后（包括 NAT 重定向等规则）会丢失，需要手动重新设置。因此，为了解决 iptables 规则在系统重启后丢失的问题，有2种常见的方法。【个人推荐方法2】

*   方法1.创建 systemd 服务来自动运行脚本：

创建脚本文件

```null
nano /root/hy2jump.sh

```

编辑脚本文件

```null
#!/bin/bash
​

iptables -t nat -A PREROUTING -i eth0 -p udp --dport 30000:50000 -j REDIRECT --to-ports 443
​

ip6tables -t nat -A PREROUTING -i eth0 -p udp --dport 30000:50000 -j REDIRECT --to-ports 443

```

> 备注：
> 
> 删除规则
> 
> `sudo iptables -t nat -D PREROUTING -i eth0 -p udp --dport 30000:50000 -j REDIRECT --to-ports 443`  
> `sudo ip6tables -t nat -D PREROUTING -i eth0 -p udp --dport 30000:50000 -j REDIRECT --to-ports 443`

给脚本赋予权限

```null
chmod +x /root/hy2jump.sh

```

将脚本添加到系统启动项

```null
echo "[Unit]
Description=hysteria2 Port Redirect
​
[Service]
ExecStart=/root/hy2jump.sh
​
[Install]
WantedBy=multi-user.target" > /etc/systemd/system/hy2jump.service

```

重新加载 systemd，并启用服务

```null

sudo systemctl daemon-reload
​

sudo systemctl start hy2jump.service
​

sudo systemctl enable hy2jump.service

```

*   ![](https://linux.do/images/emoji/twemoji/glowing_star.png?v=14)
    方法2：使用iptables-persistent包来保存和恢复规则  
    安装iptables-persistent

```null
sudo apt-get install iptables-persistent

```

安装后，你可以使用以下命令手动保存当前的规则：

```null
sudo netfilter-persistent save

```

这样，在系统重启时，iptables 规则会自动恢复。

[](#p-2099300-h-2hysteria2-12)2.重启Hysteria2服务
---------------------------------------------

重启服务。

```null
systemctl restart hysteria-server.service

```

查询服务状态。

```null
systemctl status hysteria-server.service

```

**此时我们的端口跳跃功能已经添加完毕，下面我们进入客户端的配置。** 

客户端需要与服务器端转发的端口进行相同的端口跳跃配置，以确保能够跟踪服务器的端口变化。

其他人的教程可能会将客户端的配置细化成不同的类型（比如Surge、圈X等），不过我这边比较偷懒，喜欢直接用订阅转换直接添加。

[](#p-2099300-h-1-14)1.构造节点
---------------------------

在之前的教程中，我们的节点已经搭建成功，这里假设你的VPS的IP为：**123.123.123.123**，则你的hysteria2的链接为：

```null
hysteria2://linuxdo@123.123.123.123:443?insecure=1&sni=cn.bing.com&alpn=h3

```

如果采用自签证书方法，在配置中加入 skip-cert-verify=true

```null
hysteria2://linuxdo@123.123.123.123:443?insecure=1&skip-cert-verify=true&sni=cn.bing.com&alpn=h3

```

**因此，我们在转发了相应的端口后，也只需要加入相应的端口跳跃的参数即可**，也就是ports=30000-50000。

```null
hysteria2://linuxdo@123.123.123.123:443?insecure=1&skip-cert-verify=true&sni=cn.bing.com&alpn=h3&ports=30000-50000

```

[](#p-2099300-h-2-15)2.订阅转换
---------------------------

下面我们将节点导入代理工具，以Mihimo-party为例。

将链接复制粘贴进订阅转换工具，以我自建的订阅转换工具为例。  
[Subconverter Web (yuju.love)](https://sub.yuju.love/)

[![](https://linux.do/uploads/default/optimized/3X/a/6/a66bfdc4fdadef10e973808e0f023de51c9e8630_2_690x309.png)
](https://linux.do/uploads/default/original/3X/a/6/a66bfdc4fdadef10e973808e0f023de51c9e8630.png "image")

点击转换按钮，将得到的订阅地址复制。

[](#p-2099300-mihomo-party-16)**将订阅链接导入Mihomo-party**
-----------------------------------------------------

[![](https://linux.do/uploads/default/optimized/3X/9/9/99194b89cc26c9230975deec9d16e186eb7bbdc9_2_690x219.png)
](https://linux.do/uploads/default/original/3X/9/9/99194b89cc26c9230975deec9d16e186eb7bbdc9.png "image")

**接下来就可以愉快使用啦！**

[![](https://linux.do/uploads/default/optimized/3X/3/6/365f1559d2d7b69a645a4da7752a0bd44feff7fd_2_650x500.png)
](https://linux.do/uploads/default/original/3X/3/6/365f1559d2d7b69a645a4da7752a0bd44feff7fd.png "image")

**今天的教程就到这里了，希望大家多多给我点赞~**