# Claude Code常用命令速查 - Nickey103 - 博客园
前言
--

Claude Code是Anthropic推出的AI编程助手，运行在终端中，能通过自然语言帮你编写、调试和管理代码。

### 高频命令

```null

claude --resume


claude -c


control + L


/init


开启聊天时赋予权限
claude -c --dangerously-skip-permissions
聊天时赋予权限
shift + TAB


两次 shift + TAB


在提示词中加入 ultrathink 等关键字


/model


/context


@ + 文件名


/review


control + C


cat file.py | claude -p "优化这段代码"


control + v


Option+Enter


/memory


claude config set --global preferredNotifChannel terminal_bell


control + D


npx ccusage@latest

      ccusage其他常用指令：

      
      ccusage          
      ccusage daily    
      ccusage monthly  
      ccusage session  
      ccusage blocks   

      
      ccusage blocks --live  

      
      ccusage daily --since 20250525 --until 20250530  
      ccusage daily --json      
      ccusage daily --breakdown 


！+ Bash命令




```

一、基础启动命令
--------

### 1.1 启动方式

```null

claude


claude "帮我分析这个项目结构"


claude -p "解释这个函数"


cat file.py | claude -p "优化这段代码"

```

### 1.2 常用启动参数

*   `--resume`: 恢复上次会话
*   `--plan`: 启用计划模式（适合复杂任务）
*   `--architect`: 大型项目架构模式

二、核心Slash命令
-----------

### 2.1 基础管理

```null
/help          
/clear         
/exit          
/cost          
/doctor        

```

### 2.2 项目管理

```null
/memory        
/memory view   
/config        
/init          

```

### 2.3 会话优化

```null
/compact       
/bug           
/terminal-setup 

```

三、实用技巧
------

### 3.1 CLAUDE.md文件

在项目根目录创建`CLAUDE.md`文件，Claude会自动读取：

```null
# 项目说明
这是一个React项目

## 常用命令
- 启动：npm start
- 测试：npm test
- 构建：npm run build

## 注意事项
- 使用TypeScript
- 遵循ESLint规则

```

### 3.2 Memory功能

```null

/memory
项目使用Vue3 + TypeScript
API地址：https://api.example.com
测试账号：test@example.com

```

### 3.3 自定义命令

在`.claude/commands/`目录创建`.md`文件：

```null
# debug.md
请帮我调试以下问题：$ARGUMENTS

步骤：
1. 检查错误日志
2. 分析原因
3. 提供解决方案

```

使用：`/debug "登录失败"`

四、常见使用场景
--------

### 4.1 代码调试

```null
"这个函数报错了，帮我看看问题在哪"
"为什么我的API请求失败了？"
"这个React组件渲染有问题"

```

### 4.2 代码优化

```null
"优化这段代码的性能"
"重构这个函数，让它更简洁"
"添加错误处理"

```

### 4.3 项目管理

```null
"帮我写单元测试"
"创建一个新的API接口"
"更新项目文档"
"提交代码到git"

```

五、最佳实践
------

### 5.1 高效工作流

1.  **项目启动**：创建CLAUDE.md文件
2.  **设置记忆**：使用`/memory`记录项目信息
3.  **定期清理**：使用`/clear`清除无关历史
4.  **善用自定义命令**：创建常用工作流模板

### 5.2 提问技巧

*   **明确具体**：不要说"有问题"，要说"登录接口返回500错误"
*   **提供上下文**：告诉Claude你的技术栈和项目类型
*   **分步骤**：复杂任务可以分解为多个简单步骤

### 5.3 性能优化

```null
/compact       
/clear         
/cost          

```

六、常见问题解决
--------

### 6.1 安装问题

```null

claude --version


npm install -g @anthropic/claude-code


claude /doctor

```

### 6.2 权限问题

*   确保已设置API Key
*   检查网络连接
*   验证账户状态

### 6.3 性能问题

*   定期使用`/clear`清理历史
*   使用`/compact`压缩会话
*   避免上传大文件

七、进阶技巧
------

### 7.1 团队协作

*   将`.claude/`目录提交到git
*   共享CLAUDE.md文件
*   统一自定义命令

### 7.2 多项目管理

*   不同项目使用不同的Memory设置
*   为每个项目创建专用的CLAUDE.md
*   使用项目特定的自定义命令

### 7.3 自动化工作流

```null


启动开发环境：
1. npm install
2. npm start
3. 打开浏览器访问 http://localhost:3000

```

八、实用命令速查表
---------

| 命令 | 功能 | 使用频率 |
| --- | --- | --- |
| `/help` | 查看帮助 | ⭐⭐⭐⭐⭐ |
| `/clear` | 清除历史 | ⭐⭐⭐⭐⭐ |
| `/memory` | 项目记忆 | ⭐⭐⭐⭐ |
| `/cost` | Token使用 | ⭐⭐⭐⭐ |
| `/compact` | 压缩会话 | ⭐⭐⭐ |
| `/doctor` | 系统检查 | ⭐⭐⭐ |
| `/config` | 查看配置 | ⭐⭐ |
| `/init` | 初始化项目 | ⭐⭐ |

总结
--

Claude Code是一个强大的AI编程助手，掌握这些常用命令就能处理大部分日常开发任务：

1.  **启动时**：使用`claude`进入交互模式
2.  **设置项目**：创建CLAUDE.md文件，设置Memory
3.  **日常使用**：善用自然语言描述需求
4.  **优化性能**：定期`/clear`和`/compact`
5.  **解决问题**：使用`/doctor`检查，`/help`查看帮助

记住：Claude Code最大的优势是理解自然语言，所以直接说出你的需求即可！

* * *

**相关资源：** 

*   [Claude Code官方文档](https://docs.anthropic.com/claude-code)
*   [安装指南](https://github.com/anthropics/claude-code)

**使用开发建议：**   
要求Claude在编码前制定计划。明确告诉它在您确认其计划看起来不错之前不要编码。  
按Escape中断Claude在任何阶段（思考、工具调用、文件编辑），保留上下文以便您可以纠偏或扩展指令。  
双击Escape跳回历史，编辑之前的提示词，并探索不同的方向。您可以编辑提示词并重复直到获得您要寻找的结果。  
要求Claude撤销更改，通常与选项#2结合使用以采取不同的方法。