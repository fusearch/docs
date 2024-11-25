---
weight: 109
title: API Reference

search: true
---

# 动作识别 {#Action}

识别输入内容或图像数据，返回相应的动作类型和结果。

> 代码示例：

```shell
curl -X POST 'https://api.fusearch.cn/ai/action' \
-H 'accept: application/json' \
-H 'Content-Type: application/json' \
-H 'X-API-KEY: API-KEY' \
-d '{
    "input_type": "content",
    "content": "请帮我打开教学管理菜单"
}'
```

```python
import requests

url = "https://api.fusearch.cn/ai/action"
api_key = "API-KEY"

headers = {
    "accept": "application/json",
    "Content-Type": "application/json",
    "X-API-KEY": api_key
}

data = {
    "input_type": "content",
    "content": "请帮我打开教学管理菜单"
}

response = requests.post(url, json=data, headers=headers)
print(response.json())
```

> 正确返回数据应答样例

```json
{
    "code": 0,
    "title": "好的，正在打开菜单",
    "action": "openMenu",
    "result": "教学管理菜单"
}
```

> 系统内部问题的应答案例

```json
{
    "error": "无法识别动作",
    "code": 80005
}
```

### HTTP请求

`POST https://api.fusearch.cn/ai/action`

### 请求参数

| 参数           | 描述                                                         |
|----------------|--------------------------------------------------------------|
| `input_type`   | `字符串`，输入类型，支持`content`和`image_data` |
| `content`      | `字符串`，文本内容，当`input_type`为`content`时必填 |
| `image_data`   | `字符串`，base64编码的图像数据，当`input_type`为`image_data`时必填 |

### 返回数据格式

参数 | 描述
--------- | -------
`code` | 状态码
`title` | 提示信息
`action` | 动作类型，可能的值包括`openMenuMaybe`、`error`、`openMenu`、`ocr`
`result` | 结果

### 状态码说明

status | 说明
--------- | -------
`0` | 请求成功
`80005` | 无法识别动作
