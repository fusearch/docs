---
weight: 108
title: API Reference

search: true
---

# 手语提取 {#SLExtract}

从文本中提取手语信息，返回提取结果和置信度。

> 代码示例：

```shell
curl -X POST 'https://api.fusearch.cn/ai/slextract' \
-H 'accept: application/json' \
-H 'Content-Type: application/json' \
-H 'X-API-KEY: API-KEY' \
-d '{"content": "待提取的文本内容"}'
```

```python
import requests

url = "https://api.fusearch.cn/ai/slextract"
api_key = "API-KEY"

headers = {
    "accept": "application/json",
    "Content-Type": "application/json",
    "X-API-KEY": api_key
}

data = {
    "content": "待提取的文本内容"
}

response = requests.post(url, json=data, headers=headers)
print(response.json())
```

> 正确返回数据应答样例

```json
{
    "text": "提取结果",
    "confidence": 0.95,
    "code": 0
}
```

> 系统内部问题的应答案例

```json
{
    "error": "无法提取手语",
    "code": 80003
}
```

### HTTP请求

`POST https://api.fusearch.cn/ai/slextract`

### 请求参数

| 参数           | 描述                                                         |
|----------------|--------------------------------------------------------------|
| `content`      | `字符串`，待提取的文本内容

### 返回数据格式

参数 | 描述
--------- | -------
`text` | 提取结果
`confidence` | 置信度
`code` | 状态码

### 状态码说明

status | 说明
--------- | -------
`0` | 请求成功
`80003` | 无法提取手语
