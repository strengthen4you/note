# rust desk 配置随手记录 - 资源荟萃 - LINUX DO
由 ninestep 发布于 9月 2 日
---------------------

[![](https://linux.do/user_avatar/linux.do/ninestep/48/307123_2.gif)
](https://linux.do/u/ninestep)

最近自建了rust desk 的中转服务器，但是一直无法在登录状态下链接远程主机，就在github上找解决方案。找到两种解决方案。

1.  使用s6的服务端，但是原来的设备一直无法上线，遂废弃；
2.  使用大佬编译好的客户端，但是在mac上一直无法启动，又百般检索，最后找到解决方案，特在此记录，避免下次忘了。  
    首先创建中转服务器，这里把使用的 `docker-compose.yml`附上,使用时需要自己修改秘钥和域名。

```
name: rustdesk-server
services:
  hbbs:
    command:
      - hbbs
    container_name: rustdesk-server-hbbs
    depends_on:
      - hbbr
    image: rustdesk/rustdesk-server:latest
    environment:
      - KEY=+111111111= # 如果设置了此参数，将强制使用指定密钥对，如果设为 "_"，则强制使用任意密钥；下同
    restart: unless-stopped
    volumes:
      - /DATA/AppData/rustdesk-server/data:/root
    networks:
      - rustdesk-server
    ports:
      - 21115:21115
      - 21116:21116
      - 21116:21116/udp
      - 21118:21118

  hbbr:
    command:
      - hbbr
    container_name: rustdesk-server-hbbr
    image: rustdesk/rustdesk-server:latest
    environment:
      - KEY=+111111111=
    restart: unless-stopped
    volumes:
      - /DATA/AppData/rustdesk-server/data:/root
    networks:
      - rustdesk-server
    ports:
      - 21117:21117
      - 21119:21119

  api:
    image: lejianwen/rustdesk-api:latest
    container_name: rustdesk-server-api
    environment:
      - TZ=Asia/Shanghai
      - RUSTDESK_API_APP_REGISTER=false
      - RUSTDESK_API_LANG=zh-CN
      - RUSTDESK_API_RUSTDESK_ID_SERVER=rustdesk.com:21116
      - RUSTDESK_API_RUSTDESK_RELAY_SERVER=rustdesk.com:21117
      - RUSTDESK_API_RUSTDESK_API_SERVER=http://rustdesk.com:21114
      - RUSTDESK_API_RUSTDESK_KEY=+111111111=
    ports:
      - 21114:21114
    volumes:
      - /DATA/AppData/rustdesk-server/api:/app/data
    networks:
      - rustdesk-server
    restart: unless-stopped
    depends_on:
      - hbbs
      - hbbr

networks:
  rustdesk-server:
    name: rustdesk-server

x-casaos:
  architectures:
    - arm
    - arm64
    - amd64
  main: api
  store_app_id: rustdesk-server
  category: Utilities
  author: Cp0204
  developer: rustdesk | lejianwen
  icon: https://cdn.jsdelivr.net/gh/Cp0204/CasaOS-AppStore-Play@main/Apps/rustdesk-server/icon.png
  screenshot_link:
    - https://cdn.jsdelivr.net/gh/Cp0204/CasaOS-AppStore-Play@main/Apps/rustdesk-server/screenshot-1.png
    - https://cdn.jsdelivr.net/gh/Cp0204/CasaOS-AppStore-Play@main/Apps/rustdesk-server/screenshot-2.png
    - https://cdn.jsdelivr.net/gh/Cp0204/CasaOS-AppStore-Play@main/Apps/rustdesk-server/screenshot-3.png
  thumbnail: https://cdn.jsdelivr.net/gh/Cp0204/CasaOS-AppStore-Play@main/Apps/rustdesk-server/thumbnail.png
  description:
    en_us: RustDesk builds its own transit server, combining the official [rustdesk-server](https://github.com/rustdesk/rustdesk-server) and lejianwen's [rustdesk-api](https://github.com/lejianwen/rustdesk-api).
    zh_cn: RustDesk 自建中转服务器，集合官方 [rustdesk-server](https://github.com/rustdesk/rustdesk-server) 与 lejianwen 的 [rustdesk-api](https://github.com/lejianwen/rustdesk-api) 服务。
  tagline:
    en_us: RustDesk Self-Hosted
    zh_cn: RustDesk 自托管
  title:
    en_us: RustDesk Server
  tips:
    before_install:
      en_us: The initial installation administrator is the username admin, the password will be printed on the console, you can change the password via [CLI](https://github.com/lejianwen/rustdesk-api#CLI)
      zh_cn: 初次安装管理员为用户名为admin，密码将在控制台打印，可以通过[命令行](https://github.com/lejianwen/rustdesk-api#CLI)更改密码
  port_map: "21114"
  scheme: http
  index: / 
```

遇到的问题：

1.  登录状态无法连接其他客户端  
    大佬已经有相关文章 [关于PC端链接超时或者链接不上的问题以及解决方案 | About the problem of timeout or connection failure on PC and how to solve it · Issue #92 · lejianwen/rustdesk-api · GitHub](https://github.com/lejianwen/rustdesk-api/issues/92) 可以自行浏览
2.  下载的客户端在mac无法运行
    
    1.  已损坏  
        `xattr -cr /Applications/RustDesk.app`
    2.  运行没反应
    
    ```null
    sudo spctl --master-disable
    sudo codesign --force --deep --sign - /Applications/RustDesk.app
    sudo spctl --master-enable
    
    ```
    

由 handsome 发布于 9月 2 日
---------------------

[![](https://linux.do/user_avatar/linux.do/handsome/48/736205_2.png)
](https://linux.do/u/handsome)

由 lovemiku 发布于 9月 2 日
---------------------

由 ninestep 发布于 9月 2 日
---------------------

由 zhile 发布于 9月 2 日
------------------