---
weight: 106
title: API Reference

search: true
---

# 智能问答助手 {#ChatAssistant}

基于先进的大语言模型,提供智能问答服务。可快速适配各类场景,包括客服咨询、知识问答、任务对话等,实现自动化的智能对话交互。支持多轮对话上下文理解,准确把握用户意图,提供流畅自然的对话体验。

> 代码示例：

```shell
curl -X POST 'https://api.fusearch.cn/ai/chat' \
-H 'accept: application/json' \
-H 'Content-Type: application/json' \
-H 'X-API-KEY: API-KEY' \
-d '{
    {"content": "你好"}
}'
```

```python
import requests

url = "https://api.fusearch.cn/ai/chat"
api_key = "API-KEY"

headers = {
    "accept": "application/json",
    "Content-Type": "application/json",
    "X-API-KEY": api_key
}

data = {
    "content": "你好"
}

response = requests.post(url, headers=headers, json=data)
print(response.json())
```


> 正确返回数据应答样例

```json
{
    "reply": "你好！欢迎来到我们的商场。请问有什么可以帮助您的？您是想找商店、设施，还是了解当前的促销活动？"
}
```

> 系统内部问题的应答案例

```json
{
    "status": "500",
    "message": "no response"
}
```

### HTTP请求

`POST https://api.fusearch.cn/ai/chat`

### 请求参数

| 参数           | 描述                                                         |
|----------------|--------------------------------------------------------------|
| `content`       | `字符串`，用户输入的内容。 |

### 返回数据格式

参数 | 描述
--------- | -------
`reply` | 系统回复的内容

### 状态码说明

status | 说明
--------- | -------
`200` | 请求成功
`500` | 服务器内部错误，此时`message`包含错误详情

### 返回字段数据说明

字段 | 说明
--- | ---
reply | 系统回复的内容
sl_confidence | 手语识别的置信度. 如果有此字段, 则表示系统识别出了手语, 并返回了手语识别的结果
