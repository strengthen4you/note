# Qwen Code一键启动|拒绝Vibe价格刺客反薅|爽用魔搭每日2000次请求|注意魔搭key前缀ms-导致401问题 - 开发调优 - LINUX DO
Windows教程，其他平台调整一下环境变量即可  
1.安装Qwen Code：npm install -g @qwen-code/qwen-code  
运行：qwen  
2.先不要去薅阿里云百炼的100W Tokens，看到好多佬友几个请求就被百炼的价格刺客给反薅了！**很快就倒欠阿里云100**，不愧是套路云！请打开[魔搭社区](https://modelscope.cn/)注册账号获取免费的每日2000次请求，然后来到： [访问令牌 · 魔搭社区](https://modelscope.cn/my/myaccesstoken)，默认就有一个API\_KEY，这个就是我们要配置Qwen Code的key，点击即可复制  

[![](https://linux.do/uploads/default/original/4X/3/1/4/3149c48253c06d96de491897cb6d927c6ca84fbd.png)
](https://linux.do/uploads/default/original/4X/3/1/4/3149c48253c06d96de491897cb6d927c6ca84fbd.png "image")

[](#p-7426857-api_keyapi_keyms-401-1)请注意魔搭社区似乎在调整api\_key的格式，部分佬友的api\_key可能被加上了"ms-"前缀导致401，请删除前缀尝试。以及后续可能魔搭确实会增加这个新前缀
-----------------------------------------------------------------------------------------------------------------------

3.检查魔搭社区是否绑定了阿里云账号，这一步很关键！没有绑定的话，对话时会触发401权限验证失败。打开[个人中心 · 魔搭社区](https://modelscope.cn/my/accountsettings)检查阿里云账号：  

[![](https://linux.do/uploads/default/optimized/4X/d/a/6/da6b11a0820ae745450dab19bbd885b06ecb1056_2_433x500.jpeg)
](https://linux.do/uploads/default/original/4X/d/a/6/da6b11a0820ae745450dab19bbd885b06ecb1056.jpeg "image")

**请注意一定要开通阿里云百炼权限，不开也可能401权限验证失败**  
[大模型服务平台百炼\_企业级大模型开发平台\_百炼AI应用构建-阿里云](https://www.aliyun.com/product/bailian)

4.（可省略）获取API配置参数： [通义千问3-Coder-480B-A35B-Instruct · 模型库](https://modelscope.cn/models/Qwen/Qwen3-Coder-480B-A35B-Instruct/summary)打开Qwen3-Coder的模型页面，右侧的“推理 API-Inference”卡片中点击“查看代码范例”，弹出的编辑窗中就有API\_KAY(已自动填入可用key)、BASE\_URL、MODEL这三个参数，这就是Qwen Code运行时要填写的权限信息  

[![](https://linux.do/uploads/default/optimized/4X/4/4/6/446f1f7f85a1028c678710d6f148e2d0e66382ab_2_278x499.jpeg)
](https://linux.do/uploads/default/original/4X/4/4/6/446f1f7f85a1028c678710d6f148e2d0e66382ab.jpeg "image")

5.~运行qwen并设定API\_KEY~，~设置系统环境变量~，都不用的佬，每次运行qwen填key、url、model太麻烦了，设置系统环境变量可能影响其他程序使用，我们直接来个一键启动！找一个文件夹右键->新建->快捷方式，键入对象的位置：

> C:\\Windows\\System32\\cmd.exe /k set OPENAI\_API\_KEY=****你的key****&&set OPENAI\_BASE\_URL=[https://api-inference.modelscope.cn/v1/&&set](https://api-inference.modelscope.cn/v1/&&set) OPENAI\_MODEL=Qwen/Qwen3-Coder-480B-A35B-Instruct&&qwen

注意C:\\Windows\\System32\\cmd.exe路径和OPENAI\_API\_KEY替换成自己的，然后这个快捷方式的“起始位置”**一定要留空**，这样随便拷贝这个快捷方式到任意项目目录，一键启动默认工作目录就是项目目录（Qwen Code只能操作当前目录的文件，无法跨目录操作）  

[![](https://linux.do/uploads/default/original/4X/2/7/3/27399400a8c62e6ffc9aca1b3b33e8aba7a265c0.png)
](https://linux.do/uploads/default/original/4X/2/7/3/27399400a8c62e6ffc9aca1b3b33e8aba7a265c0.png "image")

这样每次的环境变量只对当前命令行窗口生效，不会影响其他Vibe！Enjoy！

[![](https://linux.do/uploads/default/optimized/4X/e/4/4/e44f424bce034050720e35b0f09edfcf046e7c06_2_283x499.jpeg)
](https://linux.do/uploads/default/original/4X/e/4/4/e44f424bce034050720e35b0f09edfcf046e7c06.jpeg "image")

按照这个步骤做了，结果在魔搭的notebook 里都不能运行 ![](https://linux.do/images/emoji/twemoji/rofl.png?v=14)
  

[![](https://linux.do/uploads/default/optimized/4X/8/3/d/83d1b2e9fb855aafa258be1d12bd2d0774a22865_2_690x400.png)
](https://linux.do/uploads/default/original/4X/8/3/d/83d1b2e9fb855aafa258be1d12bd2d0774a22865.png "image")

佬看一下第3步绑定阿里云账号，魔搭和阿里云账号状态都正常吧？另外换一下key吧，佬这个key已经发出来了

正常呢  

[![](https://linux.do/uploads/default/optimized/4X/f/b/f/fbf61ad9698b0e97f22089fea1ec2e224d8280f1_2_475x500.jpeg)
](https://linux.do/uploads/default/original/4X/f/b/f/fbf61ad9698b0e97f22089fea1ec2e224d8280f1.jpeg "image")

感觉魔搭现在有问题，新注册的账号绑定了阿里云之后调API还是401

看楼下佬的说法可能是魔搭出问题了，可以耐心等待一下呢佬

哈哈难道是套路云发现自己被薅了不爽了 ![](https://linux.do/uploads/default/original/3X/2/e/2e09f3a3c7b27eacbabe9e9614b06b88d5b06343.png?v=14)
我是上午注册的魔搭

[![](https://linux.do/uploads/default/optimized/4X/3/c/3/3c3bf4af2f2b4fedf47d61b162778ac744f675cf_2_690x359.png)
](https://linux.do/uploads/default/original/4X/3/c/3/3c3bf4af2f2b4fedf47d61b162778ac744f675cf.png "image")

这样的佬