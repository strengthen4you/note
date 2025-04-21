# Docker/DockerHub 国内镜像源/加速列表（4月18日更新-长期维护）-腾讯云开发者社区-腾讯云
### **前言**

本列表为科研工作者提供 [docker](https://cloud.tencent.com/product/tke?from_column=20065&from=20065) 镜像网站，网络不好的同学可以使用镜像，或者推荐给身边有需要的朋友使用这些 docker 镜像。

> 注意：仅供学术研究使用。 ⚠️长期更新，建议收藏！

### **更新日志**

4 月 18 日确认可用：[https://docker.xuanyuan.me](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdocker.xuanyuan.me%2F&objectId=2485043&objectType=1&isNewArticle=undefined) （该源支持群晖 nas DMS7.2，里面有详细教程）

4 月 18 日确认可用：[https://docker.1ms.run](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdocker.xuanyuan.me%2F&objectId=2485043&objectType=1&isNewArticle=undefined)

3 月 12 该源新增了 [docker hub 镜像搜索](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdockers.xuanyuan.me&objectId=2485043&objectType=1&isNewArticle=undefined)功能：[https://dockers.xuanyuan.me](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdockers.xuanyuan.me%2F&objectId=2485043&objectType=1&isNewArticle=undefined)，方便大家搜索正确的 docker tags

3 月 1 日该源新增了[docker中文文档](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdockerdocs.xuanyuan.me%2F&objectId=2485043&objectType=1&isNewArticle=undefined)：[https://dockerdocs.xuanyuan.me](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdockerdocs.xuanyuan.me%2F&objectId=2485043&objectType=1&isNewArticle=undefined)

~11 月 25 日新增：~[~https://docker.linkedbus.com （推荐）~](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdocker.linkedbus.com%2F&objectId=2485043&objectType=1&isNewArticle=undefined)

~11 月 2 日 确认 失效：~[~https://dockerproxy.cn~](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdockerproxy.cn&objectId=2485043&objectType=1&isNewArticle=undefined)

~1 月 6 日 确认失效：~[~https://docker.rainbond.cc~](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdocker.rainbond.cc%2F&objectId=2485043&objectType=1&isNewArticle=undefined)

~1 月 6 日 确认失效：~[~https://docker.udayun.com~](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdocker.udayun.com%2F&objectId=2485043&objectType=1&isNewArticle=undefined)

~11 月 2 日 确认 失效：~[~https://docker.211678.top~](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdocker.211678.top&objectId=2485043&objectType=1&isNewArticle=undefined)

10 月 21 日新增：[https://xdark.top](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdocker.xuanyuan.me%2F&objectId=2485043&objectType=1&isNewArticle=undefined)

### **使用教程**

###### **为了加速镜像拉取，使用以下命令设置** **registry mirror**

> 支持系统：Ubuntu 16.04+、Debian 8+、CentOS 7+

代码语言：javascript

代码运行次数：0

运行

AI代码解释

复制

```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<EOF
{
    "registry-mirrors": [
        "https://docker.1ms.run",
        "https://docker.xuanyuan.me"
    ]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

###### **使用DockerHub 代理，以下以** [**docker.1ms.run**](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdocker.xuanyuan.me%2F&objectId=2485043&objectType=1&isNewArticle=undefined) **为例：可以根据列表自行替换**

代码语言：javascript

代码运行次数：0

运行

AI代码解释

复制

```
docker pull docker.1ms.run/library/mysql:5.7
```

说明：library是一个特殊的命名空间，它代表的是官方镜像。如果是某个用户的镜像就把library替换为镜像的用户名。

#### **Linux**

运行以下命令进行配置

代码语言：javascript

代码运行次数：0

运行

AI代码解释

复制

```
#!/bin/sh
cat <<-EOF > /etc/docker/daemon.json 
{
  "registry-mirrors": [
  	"https://docker.1ms.run",
  	"https://docker.xuanyuan.me"
  	]
}
EOF
systemctl daemon-reload
systemctl restart docker
```

这适用于Ubuntu 14.04、Debian、CentOS 6、CentOS 7、Fedora、Arch Linux、openSUSE Leap 42.1等系统。

#### **macOS（Docker For Mac）**

对于macOS上的Docker For Mac用户，您可以通过以下步骤配置镜像加速服务：

1、点击桌面顶栏的docker图标，选择Preferences。

2、在 Daemon 标签下的 Registry mirrors 列表中加入以下镜像地址：

代码语言：javascript

代码运行次数：0

运行

AI代码解释

复制

```
https://docker.1ms.run
https://docker.xuanyuan.me
```

3、点击Apply & Restart按钮使设置生效。

#### **Windows（Docker For Windows）**

Windows系统上的Docker For Windows用户可以按照以下步骤配置镜像加速服务：

1.  在桌面右下角状态栏中右键docker图标，修改在Docker Daemon标签页中的json。
2.  将以下地址加入"registry-mirrors"的数组里。[docker.1ms.run](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdocker.xuanyuan.me%2F&objectId=2485043&objectType=1&isNewArticle=undefined) [`https://docker.xuanyuan.me`](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fdocker.xuanyuan.me%2F&objectId=2485043&objectType=1&isNewArticle=undefined)
3.  点击Apply，重新生成Docker环境以使配置生效。

### **更多可用镜像**

| 

DockerHub镜像仓库



 | 

镜像加速器地址



 |
| --- | --- |
| 

镜像使用说明 657



 | 

[https://dockerhub.icu](https://dockerhub.icu/)（0913 测试不可用）





 |
| 

​



 | 

hub.rat.dev



 |
| 

​



 | 

docker.wanpeng.top



 |
| 

镜像使用说明 250



 | 

[https://doublezonline.cloud](https://doublezonline.cloud/)





 |
| 

镜像使用说明 76



 | 

[https://docker.mrxn.net](https://docker.mrxn.net/)（1102 测试不可用）





 |
| 

镜像使用说明 45



 | 

[https://lynn520.xyz](https://lynn520.xyz/)（1102 测试不可用）





 |
| 

镜像使用说明 30



 | 

[https://ginger20240704.asia](https://ginger20240704.asia/)（1102 测试不可用）





 |
| 

DockerHub 镜像加速代理 102



 | 

[https://docker.anyhub.us.kg](https://docker.anyhub.us.kg/)（0831测试已不可用）





 |
| 

Dockerhub镜像加速说明 70



 | 

[https://docker.wget.at](https://docker.wget.at/)（1102 测试不可用）





 |
| 

镜像使用说明 38



 | 

[https://docker.awsl9527.cn](https://docker.awsl9527.cn/)（0913 测试不可用）





 |
| 

镜像使用说明 19



 | 

[https://dislabaiot.xyz](https://dislabaiot.xyz/)





 |
| 

Docker Proxy 镜像加速 92（来源地址 22）



 | 

[https://dockerpull.com](https://dockerpull.com/)（1102 测试不可用）[https://dockerproxy.cn](https://dockerproxy.cn/)（0913 新增）（1102 测试不可用）





 |
| 

Docker Hub Container Image Library 16



 | 

[https://docker.fxxk.dedyn.io](https://docker.fxxk.dedyn.io/)





 |
| 

docker-registry-mirrors 77: 支持 Docker Hub, GitHub, Google, k8s, Quay, Microsoft 等镜像仓库.



 | 

dhub.kubesre.xyz（0913 测试不可用）



 |
| 

AtomHub 可信镜像仓库平台 27（只包含基础镜像，共336个）



 | 

[https://atomhub.openatom.cn](https://atomhub.openatom.cn/)





 |
| 

DaoCloud 镜像站 90



 | 

[https://docker.m.daocloud.io](https://docker.m.daocloud.io/)





 |
| 

已失效DockerHub镜像仓库



 | 

​



 |
| 

Docker镜像加速站 1（因流量太大，作者已关停）



 | 

[~https://hub.uuuadc.top~](https://hub.uuuadc.top/) 8（1102 测试不可用）





 |
| 

Docker镜像加速站



 | 

[~https://docker.ckyl.me~](https://docker.ckyl.me/) 4（1102 测试不可用）





 |
| 

镜像使用说明 3



 | 

[~https://docker.hpcloud.cloud~](https://docker.hpcloud.cloud/) 4（1102 测试不可用）





 |
| 

​



 | 

docker.1panel.live（1102 测试不可用）



 |
| 

​



 | 

[~https://dockerhub.jobcher.com~](https://dockerhub.jobcher.com/) 5（1102 测试不可用）





 |
| 

​



 | 

[~https://docker.chenby.cn~](https://docker.chenby.cn/) 5（1102 测试不可用）





 |

此列表只收录无需限定条件的DockerHub镜像源，感谢这些公益服务者。

### **自定义镜像源**

关于自定义镜像源，请看这篇：[Docker pull 如何自定义（指定）镜像源？](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fxuanyuan.me%2Fblog%2Farchives%2F971&objectId=2485043&objectType=1&isNewArticle=undefined)

关于自建镜像源，请看这篇：[自建 Docker 镜像摆脱 Docker pull 失败困境](https://cloud.tencent.com/developer/article/2454490?from_column=20421&from=20421)

### **Docker Compose 安装与使用教程请看：** 

[Docker Compose 安装及使用教程](https://cloud.tencent.com/developer/article/2454497?from_column=20421&from=20421)

[Dcoker Compose 模板文件详解](https://cloud.tencent.com/developer/article/2454496?from_column=20421&from=20421)

### **背景**

6月6日，[上海交大的 Docker Hub 镜像加速器](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fmirrors.ustc.edu.cn%2Fhelp%2Fdockerhub.html&objectId=2485043&objectType=1&isNewArticle=undefined) 宣布因监管要求被下架，Dockerhub 无法访问。[具体可看此通知](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fweb.archive.org%2Fweb%2F20240606081039%2Fhttps%3A%2F%2Fsjtug.org%2Fpost%2Fmirror-news%2F2024-06-06-takedown-dockerhub%2F&objectId=2485043&objectType=1&isNewArticle=undefined)。

![](https://developer.qcloudimg.com/http-save/2813964/5d08c7cc0d718ff32ac94d34064ffd3b.webp)

DockerHub 国内镜像源/加速列表