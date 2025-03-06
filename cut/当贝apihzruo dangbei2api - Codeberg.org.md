# 当贝apihzruo/dangbei2api - Codeberg.org
基于 FastAPI 的 AI 聊天服务，提供 OpenAI 兼容的 API 接口。

[](#%E4%B8%BB%E8%A6%81%E5%8A%9F%E8%83%BD)主要功能
---------------------------------------------

*   支持多种 AI 模型：
    *   DeepSeek-R1/V3
    *   Doubao
    *   Qwen
    *   以上模型均支持联网搜索版本（如 DeepSeek-R1-Search）
*   支持流式输出
*   支持多轮对话
*   支持联网搜索

[](#%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B)快速开始
---------------------------------------------

[](#%E8%BF%90%E8%A1%8C%E9%83%A8%E7%BD%B2)运行部署
---------------------------------------------

### [](#%E6%96%B9%E6%B3%95%E4%B8%80-%E7%9B%B4%E6%8E%A5%E8%BF%90%E8%A1%8C)方法一：直接运行

1.  创建并激活虚拟环境：
    
    ```
    # 创建虚拟环境
    python -m venv venv
    
    # 激活虚拟环境
    # Windows
    .\venv\Scripts\activate
    # Linux/macOS
    source venv/bin/activate 
    ```
    
2.  安装依赖：
    
    ```
    pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple 
    ```
    
3.  运行服务：
    
    ```
    # 直接运行
    python app.py
    
    # 后台运行
    nohup python app.py > output.log 2>&1 &
    
    # 查看后台进程
    ps aux | grep python
    
    # 停止服务（需要先找到进程 ID）
    kill <进程ID> 
    ```
    

### [](#%E6%96%B9%E6%B3%95%E4%BA%8C-docker-%E9%83%A8%E7%BD%B2-%E6%8E%A8%E8%8D%90)方法二：Docker 部署（推荐）

```
# 启动服务
docker-compose up -d

# 更新服务
docker-compose up -d --build

# 查看日志
docker-compose logs -f

# 停止服务
docker-compose down 
```

服务将在 [http://localhost:8000](http://localhost:8000/) 运行

[](#api-%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E)API 使用说明
-----------------------------------------------------

### [](#%E8%AE%A4%E8%AF%81)认证

所有 API 请求需要在 header 中包含有效的 API key：

```
Authorization: Bearer sk_gUXNcLwm0rnnEt55Mg8hq88 
```

### [](#%E7%A4%BA%E4%BE%8B%E8%AF%B7%E6%B1%82)示例请求

1.  获取可用模型

```
curl http://localhost:8000/v1/models \   -H "Authorization: Bearer sk_gUXNcLwm0rnnEt55Mg8hq88" 
```

2.  基础对话

```
curl http://localhost:8000/v1/chat/completions \   -H "Authorization: Bearer sk_gUXNcLwm0rnnEt55Mg8hq88" \   -H "Content-Type: application/json" \   -d '{
 "model": "DeepSeek-V3", "messages": [ {"role": "user", "content": "你好"} ] }' 
```

3.  联网搜索（使用带 Search 后缀的模型）

```
curl http://localhost:8000/v1/chat/completions \   -H "Authorization: Bearer sk_gUXNcLwm0rnnEt55Mg8hq88" \   -H "Content-Type: application/json" \   -d '{
 "model": "DeepSeek-V3-Search", "messages": [ {"role": "user", "content": "最近的新闻有哪些？"} ] }' 
```

4.  流式输出

```
curl http://localhost:8000/v1/chat/completions \   -H "Authorization: Bearer sk_gUXNcLwm0rnnEt55Mg8hq88" \   -H "Content-Type: application/json" \   -d '{
 "model": "DeepSeek-V3", "messages": [ {"role": "user", "content": "你好"} ], "stream": true }' 
```

[](#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)注意事项
---------------------------------------------

*   如有需要请修改默认的 API Key
*   确保服务器有足够的资源运行服务
*   联网搜索功能仅支持带 "-Search" 后缀的模型