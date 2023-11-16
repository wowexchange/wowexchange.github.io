
# Open-API

[中文文档](./README_zh.html),  [English API doc](./)

## 1.通用说明




该文档列出的接口除明确说明,均需要登录才可以访问,请联系我们下发token以供访问.  

连接信息如下:  
Host: `https://wowexchange.xyz/gateway-api`

验证方式:  
验证信息存放在请求头中. 名称(key)为 `token`, 值为获取到的token.
CURL参考:
```sh
curl -X GET -H  "Accept:*/*" -H  "token:S0N......6AJ" "https://wowexchange.xyz/gateway-api/spot/open-api/v1/wallets"
```

响应结果说明: 
请求成功后返回结构如下,  
```javascript
{
    "code": 200,          //响应业务代码, 200 表示成功
    "msg": "",            //错误消息,非错误情况下是""
    "data": 0             //业务结果,根据请求不同结果也不同. 详见各接口说明
}
```

特别说明:  
大数字和浮点数在返回的json中使用字符串的形式传递是为了避免数字在传递过程中丢失精度.




## 2.现货下单接口


**接口地址**: `/spot/open-api/v1/exchange/order`


**请求方式**: <code class="method_post">POST</code>


**请求数据类型**: `application/json`


**响应数据类型**: `application/json`


**接口描述**:


现货下单接口, 下单失败时错误原因在 `msg` 字段中.   
`type` 字段为下单类型, 允许2个值  
- 0 : 市价
- 1 : 限价



**请求示例**:


```json
{
  "type": 0,
  "amount": 0,
  "symbol": "BTC-USDT",
  "direction": 0,
  "price": 0,
  "useDiscount": 0
}
```


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|orderRequestDTO|下单请求参数|body|true| | |
|&emsp;&emsp;type|下单类型,可用值: 0:市价; 1:限价||true|int||
|&emsp;&emsp;amount|购买或出售总额||true|number||
|&emsp;&emsp;symbol|交易对. 格式：BTC-USDT||true|string||
|&emsp;&emsp;direction|下单方向,可用值: 0:买; 1:卖||true|int||
|&emsp;&emsp;price|价格||true|number||
|&emsp;&emsp;useDiscount|是否使用折扣,可用值: 0:不使用; 1:使用||true|int||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK| |


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code||int|int|
|msg||string||
|data| 订单ID |string||


**响应示例**:
```json
{
    "code": 200,
    "msg": "",
    "data": "5j7bsi..."
}
```


## 3.获取钱包账户列表


**接口地址**: `/spot/open-api/v1/wallets`


**请求方式**: <code class="method_get" style="">GET</code>


**响应数据类型**: `application/json`


**接口描述**:



获取当前用户的所有钱包信息  






**请求参数**:


暂无


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code||int|int|
|msg||string||
|data||array| |
|&emsp;&emsp;id|ID|string||
|&emsp;&emsp;userId|用户ID|string||
|&emsp;&emsp;coin|币种|string||
|&emsp;&emsp;coinId|币种|string||
|&emsp;&emsp;freeAmount|可用数量|number||
|&emsp;&emsp;freezeAmount|冻结数量|number||
|&emsp;&emsp;status|账户状态: 激活active, 冻结freeze|string||
|&emsp;&emsp;freeUSDTAmount|可用数量相等的USDT数量|number||
|&emsp;&emsp;freezeUSDTAmount|冻结数量相等的USDT数量|number||
|&emsp;&emsp;coinLogo|币种图标地址|string||
|&emsp;&emsp;coinDecimal|货币精度|int||



**响应示例**:
```json
{
    "code": 200,
    "msg": "",
    "data": [
        {
            "id": "",
            "userId": "",
            "coin": "",
            "coinId": "",
            "freeAmount": 0,
            "freezeAmount": 0,
            "status": "",
            "freeUSDTAmount": 0,
            "freezeUSDTAmount": 0,
            "coinLogo": "",
            "coinDecimal": 0
        }
    ]
}
```


## 4.获取交易对最新价格


**接口地址**: `/spot/open-api/v1/last-price/{symbol}`


**请求方式**: <code class="method_get" style="">GET</code>


**响应数据类型**: `application/json`


**接口描述**:


获取指定交易对的实时价格,此接口的响应 `data` 是最新价格.





**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|symbol|交易对, 格式：BTC-USDT|path|true|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code||int|int|
|msg||string||
|data|交易对的当前价格|number||


**响应示例**:
```json
{
    "code": 200,
    "msg": "",
    "data": "3968.2"
}
```


## 5.获取实时K线数据


**接口地址**: `/spot/open-api/v1/k-line/{symbol}/{interval}`


**请求方式**: <code class="method_get" style="">GET</code>


**响应数据类型**: `application/json`


**接口描述**:







**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|symbol|交易对, 格式：BTC-USDT|path|true|string||
|interval|K线间隔, 可用值: M1,M5,M15,M30,H1,H4,D1,W1,MON1|path|true|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK| |


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code||integer(int32)|integer(int32)|
|msg||string||
|data||KlineSubscribeData|KlineSubscribeData|
|&emsp;&emsp;s|交易对|string||
|&emsp;&emsp;i|时间间隔|string||
|&emsp;&emsp;dd|k线数据|KLineRespData|KLineRespData|
|&emsp;&emsp;&emsp;&emsp;o|开始价格|string||
|&emsp;&emsp;&emsp;&emsp;h|高位价格|string||
|&emsp;&emsp;&emsp;&emsp;l|地位价格|string||
|&emsp;&emsp;&emsp;&emsp;c|结束价格|string||
|&emsp;&emsp;&emsp;&emsp;h24|近24小时最高价|string||
|&emsp;&emsp;&emsp;&emsp;l24|近24小时最低价|string||
|&emsp;&emsp;&emsp;&emsp;v24|近24小时成交量|string||
|&emsp;&emsp;&emsp;&emsp;vv24|近24小时成交额|string||
|&emsp;&emsp;&emsp;&emsp;p24|24小时价格变动比|string||
|&emsp;&emsp;&emsp;&emsp;cp|24小时价格变动量|string||
|&emsp;&emsp;&emsp;&emsp;v|成交量|string||
|&emsp;&emsp;&emsp;&emsp;vv|成交额|string||
|&emsp;&emsp;&emsp;&emsp;pt|时间区间|integer||
|&emsp;&emsp;&emsp;&emsp;sse|k线无需关心此值|string||
|&emsp;&emsp;&emsp;&emsp;sos|k线无需关心此值|string||


**响应示例**:
```json
{
	"code": 0,
	"msg": "",
	"data": {
		"s": "",
		"i": "",
		"dd": {
			"o": "",
			"h": "",
			"l": "",
			"c": "",
			"h24": "",
			"l24": "",
			"v24": "",
			"vv24": "",
			"p24": "",
			"cp": "",
			"v": "",
			"vv": "",
			"pt": 0,
			"sse": "",
			"sos": ""
		}
	}
}
```


## 6.获取交易对最新交易信息


**接口地址**: `/spot/open-api/v1/exchange/{symbol}/recent-trades`


**请求方式**: <code class="method_get" style="">GET</code>


**响应数据类型**: `application/json`


**接口描述**:







**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|symbol|交易对, 格式：BTC-USDT|path|true|string||
|count|交易记录数,最大100|query|true|int||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK| |


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code||int|int|
|msg||string||
|data||object |  |
|&emsp;&emsp;s|交易对|string||
|&emsp;&emsp;ps|记录数量|int||
|&emsp;&emsp;i|交易记录列表|array| |
|&emsp;&emsp;&emsp;&emsp;a|数量|number||
|&emsp;&emsp;&emsp;&emsp;p|价格|number||
|&emsp;&emsp;&emsp;&emsp;d|交易方向, 0:买, 1:卖|int||
|&emsp;&emsp;&emsp;&emsp;t|交易成交时间|long||


**响应示例**:
```json
{
    "code": 0,
    "msg": "",
    "data": {
        "s": "",
        "ps": 0,
        "i": [
            {
                "a": 0,
                "p": 0,
                "d": 0,
                "t": 0
            }
        ]
    }
}
```


## 7.获取实时盘口数据


**接口地址**: `/spot/open-api/v1/exchange/{symbol}/partial`


**请求方式**: <code class="method_get" style="">GET</code>


**响应数据类型**: `application/json`


**接口描述**:


获取指定交易对的买盘和卖盘数据,每个盘返回的最大记录数量为`depth`,最大20档.




**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|symbol|交易对, 格式：BTC-USDT|path|true|string||
|depth|盘口的档数,买盘和卖盘分别计算,最大20|query|true|int||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK| |


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code||int|int|
|msg||string||
|data||object| |
|&emsp;&emsp;s|交易对|string||
|&emsp;&emsp;a|买盘|array| |
|&emsp;&emsp;&emsp;&emsp;p|价格|number||
|&emsp;&emsp;&emsp;&emsp;a|数量|number||
|&emsp;&emsp;&emsp;&emsp;t|总额|number||
|&emsp;&emsp;b|买盘|array| |
|&emsp;&emsp;&emsp;&emsp;p|价格|number||
|&emsp;&emsp;&emsp;&emsp;a|数量|number||
|&emsp;&emsp;&emsp;&emsp;t|总额|number||


**响应示例**:  

```json
{
    "code": 0,
    "msg": "",
    "data": {
        "s": "",
        "a": [
            {
                "p": 0,
                "a": 0,
                "t": 0
            }
        ],
        "b": [
            {
                "p": 0,
                "a": 0,
                "t": 0
            }
        ]
    }
}
```
