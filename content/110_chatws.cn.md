---
weight: 110
title: WebSocket API Reference

search: true
---

# WebSocket智能问答助手 {#WebSocketChatAssistant}

基于WebSocket协议的实时智能问答服务。相比HTTP接口,WebSocket可以保持长连接,实现双向实时通信,特别适合语音对话等场景。支持文本和语音输入,并提供语音合成功能。

> 代码示例：

```javascript
const ws = new WebSocket('wss://api.fusearch.cn/ai/chat_ws');

// 发送文本消息
ws.send(JSON.stringify({
    data_type: "text",
    content: "你好"
}));

// 发送语音数据
ws.send(JSON.stringify({
    data_type: "audio"
}));
// 紧接着发送二进制语音数据
ws.send(audioData); // audioData为二进制音频数据

// 接收消息
ws.onmessage = function(event) {
    if(typeof event.data === 'string') {
        // 处理JSON响应
        const response = JSON.parse(event.data);
        console.log('收到文本回复:', response.reply);
        
        if(response.has_audio) {
            // 等待接收音频数据
        }
    } else {
        // 处理二进制音频数据
        const audioBlob = event.data;
        // 播放音频...
    }
};
```

```python
import websockets
import json
import asyncio

async def chat():
    uri = "wss://api.fusearch.cn/ai/chat_ws"
    async with websockets.connect(uri) as websocket:
        # 发送文本消息
        await websocket.send(json.dumps({
            "data_type": "text",
            "content": "你好"
        }))
        
        # 接收JSON响应
        response = await websocket.recv()
        response_data = json.loads(response)
        print(f"收到回复: {response_data['reply']}")
        
        if response_data.get('has_audio'):
            # 接收音频数据
            audio_data = await websocket.recv()
            # 处理音频数据...

asyncio.get_event_loop().run_until_complete(chat())
```

### WebSocket连接

`WSS wss://api.fusearch.cn/ai/chat_ws`

### 请求参数

| 参数           | 描述                                                         |
|----------------|--------------------------------------------------------------|
| `data_type`    | `字符串`，输入类型。可选值：<br>`text`: 文本输入<br>`audio`: 语音输入<br>`audioFileUrl`: 语音文件URL |
| `content`      | `字符串`，当data_type为text时的文本内容 |
| `audio_data`   | `字符串`，当data_type为audio时的语音数据,不用base64编码 |

### 返回数据格式

参数 | 描述
--------- | -------
`content` | 用户输入内容的文本形式(语音输入会转换为文本)
`reply` | 系统的回复内容
`has_audio` | 布尔值,表示是否有后续的音频数据
`code` | 状态码,0表示成功
`sl_confidence` | 可选字段,手语识别的置信度
`error` | 当发生错误时的错误信息

返回数据分为两部分：
1. JSON格式的响应数据，包含上述字段
2. 当`has_audio`为true时，紧随其后会返回二进制音频数据

示例JSON响应：
```json
{
    "content": "你好",
    "reply": "你好！很高兴为您服务。",
    "has_audio": true,
    "code": 0
}
```

### 错误码说明

code | 说明
--------- | -------
`0` | 成功
`80001` | 语音识别失败
`80002` | 语音合成失败

### 通信流程

1. 客户端发送JSON格式的请求数据
2. 如果是语音输入(data_type="audio"),紧接着发送二进制语音数据
3. 服务器返回JSON格式的响应数据
4. 如果has_audio为true,服务器会紧接着发送二进制音频数据

### 注意事项

- WebSocket连接需要在header中携带`X-API-KEY`进行认证
- 语音数据建议使用16k采样率的PCM格式
- 建议处理WebSocket断开重连的情况
