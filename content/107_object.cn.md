---
weight: 107
title: API Reference

search: true
---

# 图像识别 {#ImageRecognition}

识别图像中的物体，返回详细分类统计和大类统计。

> 代码示例：

```shell
curl -X POST 'https://api.fusearch.cn/ai/object' \
-H 'accept: application/json' \
-H 'Content-Type: application/json' \
-H 'X-API-KEY: API-KEY' \
-d '{"image_data": "BASE64_ENCODED_IMAGE"}'
```

```python
import requests
import base64

url = "https://api.fusearch.cn/ai/object"
api_key = "API-KEY"

headers = {
    "accept": "application/json",
    "Content-Type": "application/json",
    "X-API-KEY": api_key
}

with open("image_path", "rb") as image_file:
    image_base64 = base64.b64encode(image_file.read()).decode('utf-8')

post_data = {
    "image_data": image_base64
}

response = requests.post(url, json=post_data, headers=headers)
print(response.json())
```

> 正确返回数据应答样例

```json
{
    "detailed_count": {
        "青苹果": 1,
        "杨桃": 1,
        "梨": 1,
        "青桔": 1
    },
    "general_count": {
        "苹果": 1,
        "杨桃": 1,
        "梨": 1,
        "青桔": 1
    },
    "confidence": 1.0,
    "code": 0
}
```

> 系统内部问题的应答案例

```json
{
    "error": "图像识别失败",
    "code": 80004
}
```

### HTTP请求

`POST https://api.fusearch.cn/ai/object`

### 请求参数

| 参数           | 描述                                                         |
|----------------|--------------------------------------------------------------|
| `image_data`   | `字符串`，要分析的图片的Base64编码

### 返回数据格式

参数 | 描述
--------- | -------
`detailed_count` | 详细分类统计
`general_count` | 大类统计
`confidence` | 置信度
`code` | 状态码

### 状态码说明

status | 说明
--------- | -------
`0` | 请求成功
`80004` | 图像识别失败
