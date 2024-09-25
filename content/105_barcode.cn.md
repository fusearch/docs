---
weight: 105
title: API Reference

search: true
---

# 条形码识别 {#Barcode}

识别图片中的一个或者多个条形码

> 代码示例：

```shell
curl -X POST 'https://api.fusearch.cn/ai/barcode' \
-H 'accept: application/json' \
-H 'Content-Type: application/json' \
-H 'X-API-KEY: API-KEY' \
-d '{"image_b64": "BASE64_ENCODE_VALUE"}'
```

```python
import requests
import base64
import json

url = "https://api.fusearch.cn/ai/barcode"
api_key = "API-KEY"

headers = {
    "accept": "application/json",
    "Content-Type": "application/json",
    "X-API-KEY": api_key
}


image_content = open(image_path, "rb").read()
image_base64 = base64.b64encode(image_content).decode('utf-8')
post_data = {
    "image_base64": image_base64
}

response = requests.post(url, json=post_data, headers=headers)
print(response.json())
```


> 正确返回数据应答样例

```json
{
	"barcodes": [{
		"data": "0485",
		"coordinates": {
			"x": 94,
			"y": 11,
			"width": 614,
			"height": 118
		}
	},{
		"data": "0865",
		"coordinates": {
			"x": 91,
			"y": 1,
			"width": 16,
			"height": 18
		}
	}]
}
```

> 获取不到请求图片的应答案例

```json
{
    "status": "400",
    "message": "no image"
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

`POST https://api.fusearch.cn/ai/barcode`

### 请求参数

| 参数           | 描述                                                         |
|----------------|--------------------------------------------------------------|
| `image_base64` | `字符串`，要分析的图片的Base64编码

### 返回数据格式

参数 | 描述
--------- | -------
`status` | 状态码
`message` | `data`：二维码内容
 | `coordinates`：二维码坐标

### 状态码说明

status | 说明
--------- | -------
`200` | 请求成功
`400` | 请求失败，参数错误或图片无法获取，此时`message`包含具体错误信息
`500` | 服务器内部错误，此时`message`包含错误详情
