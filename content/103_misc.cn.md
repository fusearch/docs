---
weight: 103
title: API Reference

search: true
---

# 图像生成文本👁️‍🗨️

基于BriVL (Bridging Vision and Language Model)的图像生成文本模型。

> 代码示例：

```python
import sdk

api = sdk.client('YOUR_ACCESS_KEY', 'YOUR_SECRET_KEY')
data = data = {"img": "BASE64_ENCODE_VALUE"}
url = "https://wenlanapi.iir.ac.cn/v1/image2text"
response = api.request(url, data)
print(response)
```

```php
<?php
require_once "crawlerclub/Client.php";

$client = new Client("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY");
$url = "https://wenlanapi.iir.ac.cn/v1/image2text";
$data = array("img"=>"BASE64_ENCODE_VALUE");
$response = $client->request($url, $data);
print($response);
```

```java
import java.util.HashMap;
import java.util.Map;
import club.crawler.Client;

public class MainClass {
    public static void main(String[] args) {
        Client api = new Client("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY");
        Map<String, String> data = new HashMap<>();
        data.put("img", "BASE64_ENCODE_VALUE");
        String url = "https://wenlanapi.iir.ac.cn/v1/image2text";
        String response = client.request(url, data);
        System.out.println(response);
    }
}
```

```go
package main

import (
    "fmt"
    "crawler.club/gosdk"
)

func main() {
    api := gosdk.NewClient("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY")
    data := map[string]string{
        "img": "BASE64_ENCODE_VALUE",
    }
    url := "https://wenlanapi.iir.ac.cn/v1/image2text"
    response, _ := api.Request(url, data)
    fmt.Println(response)
}
```

> 正确返回数据应答样例

```json
{
  "status": "SUCCESS",
  "message": {
    "text": "一个戴眼镜的年轻人的肖像",
    "type": "text",
    "score": 0.731838774222594
  }
}

```

> 图片超过2M应答样例

```json
{
  "status":"FAIL",
  "message":"No more than 2mb!"
}
```

### HTTP请求

`POST https://wenlanapi.iir.ac.cn/v1/image2text`

### 请求参数

参数 | 描述
--------- | -------
`img` | `字符串`，base64编码图片  

### 返回数据格式

参数 | 描述
--------- | -------
`status` | 状态码
`message` | `type`：返回类型，`text`为文本语句，`tags`为文本标签
 | `text`：如果`type`为`text`则有此字段，保存图片生成的文本语句
 | `tags`：如果`type`为`tags`则有此字段，保存图片生成的文本标签
 | `score`：图片生成文本的置信度，为0～1之间的小数

### 状态码说明

status | 说明
--------- | -------
`SUCCESS` | 查找成功
`FAIL` | 失败，此时`message`保存错误信息

# PM2.5空气质量指数☁️

支持全国300多个城市的空气质量指数（AQI）查询，返回各观测站PM2.5、PM10、一氧化碳、二氧化氮、臭氧、二氧化硫等分指数信息，每小时更新一次。

> 代码示例：

```python
import sdk

api = sdk.client('YOUR_ACCESS_KEY', 'YOUR_SECRET_KEY')
data = {"city": "beijing", "time": "2018051209"}
url = "https://api.crawler.club/pm25"
response = api.request(url, data)
print(response)
```

```php
<?php
require_once "crawlerclub/Client.php";

$client = new Client("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY");
$url = "https://api.crawler.club/pm25";
$data = array("city"=>"beijing", "time"=>"2018051209");
$response = $client->request($url, $data);
print($response);
```

```java
import java.util.HashMap;
import java.util.Map;
import club.crawler.Client;

public class MainClass {
    public static void main(String[] args) {
        Client api = new Client("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY");
        Map<String, String> data = new HashMap<>();
        data.put("city", "beijing");
        data.put("time", "2018051209");
        String url = "https://api.crawler.club/pm25";
        String response = client.request(url, data);
        System.out.println(response);
    }
}
```

```go
package main

import (
    "fmt"
    "crawler.club/gosdk"
)

func main() {
    api := gosdk.NewClient("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY")
    data := map[string]string{
        "city": "beijing",
        "time": "2018051209",
    }
    url := "https://api.crawler.club/pm25"
    response, _ := api.Request(url, data)
    fmt.Println(response)
}
```

> 正确返回数据应答样例

```json
{
  "status":"ok",
  "message":{
    "city_id":"beijing",
    "city":"北京",
    "update_time":"2018-05-12T09:00:00+08:00",
    "stations":[
      {
        "aqi":"269",
        "co":"2.3",
        "no2":"55",
        "o3":"31",
        "o3_8h":"8",
        "pm10":"_",
        "pm2_5":"219",
        "position_name":"海淀区万柳",
        "primary_pollutant":"细颗粒物(PM2.5)",
        "quality":"重度污染",
        "so2":"5"
      },
      {
        "aqi":"260",
        "co":"2.3",
        "no2":"59",
        "o3":"11",
        "o3_8h":"3",
        "pm10":"_",
        "pm2_5":"210",
        "position_name":"奥体中心",
        "primary_pollutant":"细颗粒物(PM2.5)",
        "quality":"重度污染",
        "so2":"2"
      }
    ]
  }
}
```

> 数据不存在应答样例

```json
{
  "status":"fail",
  "message":"data not found"
}
```

### HTTP请求

`POST https://api.crawler.club/pm25`

### 请求参数

参数 | 描述
--------- | -------
`city` | `字符串`，要查询的城市
`time` | `可选`，`字符串`，格式为`YYYYMMDDHH`

### 返回数据格式

参数 | 描述
--------- | -------
`status` | 状态码
`message` | `city_id`：城市拼音
 | `city`：城市中文名称
 | `update_time`：数据时间
 | `stations`：此城市各个监测站具体数据

### 状态码说明

status | 说明
--------- | -------
`ok` | 查找成功
`fail` | 失败，此时`message`保存错误信息

### 监测点数据说明

数值单位：`μg/m3`（`CO`为`mg/m3`）

字段 | 说明
--- | ---
position_name|监测点
aqi|`AQI`
quality|空气质量/指数类别
primary_pollutant|首要污染物
pm2_5|`PM2.5`/细颗粒物
pm10|`PM10`/可吸入颗粒物
co|`CO`/一氧化碳
no2|`NO2`/二氧化氮
o3|`O3`/臭氧1小时平均
o3_8h|`O3`/臭氧8小时平均
so2|`SO2`/二氧化硫

# 全球电话运营商归属地查询☎️

全球电话运营商归属地查询，上亿条数据量，更新及时、准确度高，数据权威。

> 代码示例：

```python
import sdk

api = sdk.client('YOUR_ACCESS_KEY', 'YOUR_SECRET_KEY')
data = {"number": "13800138000", "country": "CN"}
url = "https://api.crawler.club/phone"
response = api.request(url, data)
print(response)
```

```php
<?php
require_once "crawlerclub/Client.php";

$client = new Client("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY");
$url = "https://api.crawler.club/phone";
$data = array("number"=>"13800138000", "country"=>"CN");
$response = $client->request($url, $data);
print($response);
```

```java
import java.util.HashMap;
import java.util.Map;
import club.crawler.Client;

public class MainClass {
    public static void main(String[] args) {
        Client api = new Client("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY");
        Map<String, String> data = new HashMap<>();
        data.put("number", "13800138000");
        data.put("country", "CN");
        String url = "https://api.crawler.club/phone";
        String response = client.request(url, data);
        System.out.println(response);
    }
}
```

```go
package main

import (
    "fmt"
    "crawler.club/gosdk"
)

func main() {
    api := gosdk.NewClient("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY")
    data := map[string]string{
        "number":  "13800138000",
        "country": "CN",
    }
    url := "https://api.crawler.club/phone"
    response, _ := api.Request(url, data)
    fmt.Println(response)
}
```

> 正确返回数据应答样例

```json
{
  "status":"ok",
  "message":{
    "country_code":86,
    "national_number":13800138000,
    "is_valid_number":true,
    "number_type":"MOBILE",
    "e164":"+8613800138000",
    "region_code":"CN",
    "location":{
      "en":"Beijing",
      "zh":"北京市"
    },
    "time_zones":[
      "Asia/Shanghai"
    ],
    "carrier":{
      "en":"China Mobile",
      "zh":"中国移动"
    }
  }
}
```

> 请求错误应答样例

```json
{
  "status":"fail",
  "message":"The phone number supplied is not a number."
}
```

### HTTP请求

`POST https://api.crawler.club/phone`

### 请求参数

参数 | 描述
--------- | -------
`number` | `字符串`，要查询的电话号码
`country` | `可选`，`字符串`，国家码，默认为`CN`中国🇨🇳

### 状态码说明

status | 说明
--------- | -------
`ok` | 查找成功
`fail` | 失败，此时`message`保存错误信息

### 电话号码信息说明

字段 | 说明
--- | ---
country_code|国家代码，比如中国为`86`
national_number|国内呼叫号码
is_valid_number|是否合法电话号码
number_type|号码类型，`MOBILE`、`FIXED_LINE`
e164|`e164`格式化号码
region_code|区域代码，比如中国为`CN`
location|归属地，*多语种*
time_zones|时区
carrier|运营商，*多语种*

# 全语种网页正文抽取📑

对文章类网页抽取正文、标题、发布时间、正文图片、作者、语种、地区、关键词等信息，支持全球各语种网站。

> 代码示例：

```python
import sdk

api = sdk.client('YOUR_ACCESS_KEY', 'YOUR_SECRET_KEY')
data = {"url": "https://news.qq.com/a/20180517/001214.htm"}
url = "https://api.crawler.club/htmlextract"
response = api.request(url, data)
print(response)
```

```php
<?php
require_once "crawlerclub/Client.php";

$client = new Client("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY");
$url = "https://api.crawler.club/htmlextract";
$data = array("url"=>"https://news.qq.com/a/20180517/001214.htm");
$response = $client->request($url, $data);
print($response);
```

```java
import java.util.HashMap;
import java.util.Map;
import club.crawler.Client;

public class MainClass {
    public static void main(String[] args) {
        Client api = new Client("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY");
        Map<String, String> data = new HashMap<>();
        data.put("url", "https://news.qq.com/a/20180517/001214.htm");
        String url = "https://api.crawler.club/htmlextract";
        String response = client.request(url, data);
        System.out.println(response);
    }
}
```

```go
package main

import (
    "fmt"
    "crawler.club/gosdk"
)

func main() {
    api := gosdk.NewClient("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY")
    data := map[string]string{
        "url":  "https://news.qq.com/a/20180517/001214.htm",
    }
    url := "https://api.crawler.club/htmlextract"
    response, _ := api.Request(url, data)
    fmt.Println(response)
}
```

> 正确返回数据应答样例

```json
{
  "status":"ok",
  "message":{
    "url":"https://news.qq.com/a/20180517/001214.htm",
    "from":"qq.com",
    "site_info":{
      "Flag":1,
      "Sub":"news",
      "Root":"qq",
      "Tld":"com"
    },
    "canonical_url":"",
    "title":"国家重点研发计划立项密集发布 16专项经费51亿元",
    "text":"资料图：图为世界上首颗量子科学实验卫星“墨子号”模型。(资料图片)中新社记者 韩苏原 摄
随着“高性能计算”、“增材制造与激光制造”等重点专项拟资助项目相继公示，2018年度国家重点研发计划立项工作拉开了大幕。《经济参考报》记者16日从科技部获悉，近期三个批次的项目清单密集发布，涉及高新技术和基础研究领域在内的16个专项237个项目，国拨经费共计51亿元，其中量子调控与量子信息、纳米技术和新能源汽车等领域成为未来科研经费重点投向。
...",
    "html":"<p><img src=\"http://inews.gtimg.com/newsapp_bt/0/3603873903/641\" /></p>
<p>资料图：图为世界上首颗量子科学实验卫星“墨子号”模型。(资料图片)中新社记者 韩苏原 摄</p>
<p>随着“高性能计算”、“增材制造与激光制造”等重点专项拟资助项目相继公示，2018年度国家重点研发计划立项工作拉开了大幕。《经济参考报》记者16日从科技部获悉，近期三个批次的项目清单密集发布，涉及高新技术和基础研究领域在内的16个专项237个项目，国拨经费共计51亿元，其中量子调控与量子信息、纳米技术和新能源汽车等领域成为未来科研经费重点投向。</p>
...",
    "language":"cmn",
    "location":"CN",
    "favicon":"https://mat1.gtimg.com/www/icon/favicon2.ico",
    "images":[
      "http://inews.gtimg.com/newsapp_bt/0/3603873903/641"
    ],
    "tags":"国家重点研发计划立项密集发布 16专项经费51亿元,新能源,科技部,高技术",
    "author":"",
    "publish_date":"2018-05-17T04:02:00+08:00"
  }
}
```

> 请求错误应答样例

```json

{
  "status":"fail",
  "message":"error infomation"
}

```

### HTTP请求

`POST https://api.crawler.club/htmlextract`

### 请求参数

参数 | 描述
--------- | -------
`url` | `字符串`，要进行正文抽取的网页URL

### 状态码说明

status | 说明
--------- | -------
`ok` | 查找成功
`fail` | 失败，此时`message`保存错误信息

### 正文信息说明

字段 | 说明
--- | ---
url|网页URL
title|文章标题
text|文章正文
html|文章正文，HTML版本
publish_date|发布时间
images|正文图片
language|网页语言
location|国家，`ISO 3166-1 alpha-2 Country Codes`
author|作者
tags|关键词

# 全球银行卡校验与信息查询💳

查询全球银行卡的基本信息，包括发卡银行名称、网址、银行卡类型及有效性。

> 代码示例：

```python
import sdk

api = sdk.client('YOUR_ACCESS_KEY', 'YOUR_SECRET_KEY')
data = {"id": "6222000200124846494"}
url = "https://api.crawler.club/bankcard"
response = api.request(url, data)
print(response)
```

```php
<?php
require_once "crawlerclub/Client.php";

$client = new Client("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY");
$url = "https://api.crawler.club/bankcard";
$data = array("id"=>"6222000200124846494");
$response = $client->request($url, $data);
print($response);
```

```java
import java.util.HashMap;
import java.util.Map;
import club.crawler.Client;

public class MainClass {
    public static void main(String[] args) {
        Client api = new Client("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY");
        Map<String, String> data = new HashMap<>();
        data.put("id", "6222000200124846494");
        String url = "https://api.crawler.club/bankcard";
        String response = client.request(url, data);
        System.out.println(response);
    }
}
```

```go
package main

import (
    "fmt"
    "crawler.club/gosdk"
)

func main() {
    api := gosdk.NewClient("YOUR_ACCESS_KEY", "YOUR_SECRET_KEY")
    data := map[string]string{
        "id":  "6222000200124846494",
    }
    url := "https://api.crawler.club/bankcard"
    response, _ := api.Request(url, data)
    fmt.Println(response)
}
```

> 正确返回数据应答样例

```json

{
  "status":"ok",
  "message":{
    "name":"icbc",
    "country":"cn",
    "localTitle":"中国工商银行",
    "engTitle":"Industrial and Commercial Bank of China",
    "url":"http://www.icbc.com.cn",
    "color":"#c90000",
    "card_type":"dc",
    "length":19,
    "prefixes":0,
    "number":"6222000200124846494",
    "detail":"工商银行·灵通卡"
  }
}
```

> 请求错误应答样例

```json
{
  "status":"fail",
  "message":"invalid card number"
}
```

### HTTP请求

`POST https://api.crawler.club/bankcard`

### 请求参数

参数 | 描述
--------- | -------
`id` | `字符串`，要查询的银行卡号

### 状态码说明

status | 说明
--------- | -------
`ok` | 查找成功
`fail` | 失败，此时`message`保存错误信息

### 银行卡号信息说明

字段 | 说明
--- | ---
number|银行卡号
name|银行卡Code
country|银行卡所属国家码
localTitle|银行名字，本地语言
engTitle|银行名字，英语
url|银行网址
color|银行颜色
card_type|银行卡类型
detail|银行卡详情
