
# Open-API

[中文文档](./README_zh.html),  [English API doc](./)

## 1.通用说明
Host: `https://wowexchange.xyz/gateway-api`



## 2.现货下单接口


**接口地址**: `/spot/open-api/v1/exchange/order`


**请求方式**: <code class="method_post" style="">POST</code>


**请求数据类型**: `application/json`


**响应数据类型**: `application/json`


**接口描述**:


**请求示例**:


```json
{
  "type": "",
  "amount": 0,
  "symbol": "BTC-USDT",
  "direction": "",
  "price": 0,
  "useDiscount": 0
}
```


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|orderRequestDTO|下单请求参数|body|true| | |
|&emsp;&emsp;type|提单类型,可用值:MARKET_PRICE,LIMIT_PRICE||true|string||
|&emsp;&emsp;amount|购买或出售总额||true|number||
|&emsp;&emsp;symbol|交易对. 格式：BTC-USDT||true|string||
|&emsp;&emsp;direction|下单方向,可用值:BUY,SELL||true|string||
|&emsp;&emsp;price|价格||true|number||
|&emsp;&emsp;useDiscount|是否使用折扣,0:不使用; 1:使用||true|integer(int32)||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK| |


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code||integer(int32)|integer(int32)|
|msg||string||
|data||number||


**响应示例**:
```json
{
	"code": 0,
	"msg": "",
	"data": 0
}
```


## 3.获取钱包账户列表


**接口地址**: `/spot/open-api/v1/wallets`


**请求方式**: <code class="method_get" style="">GET</code>


**请求数据类型**: `application/x-www-form-urlencoded`


**响应数据类型**: `application/json`


**接口描述**:


**请求参数**:


暂无


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code||integer(int32)|integer(int32)|
|msg||string||
|data||number||


**响应示例**:
```json
{
	"code": 0,
	"msg": "",
	"data": 0
}
```


## 4.获取交易对最新价格


**接口地址**: `/spot/open-api/v1/last-price/{symbol}`


**请求方式**: <code class="method_get" style="">GET</code>


**请求数据类型**: `application/x-www-form-urlencoded`


**响应数据类型**: `application/json`


**接口描述**:


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
|code||integer(int32)|integer(int32)|
|msg||string||
|data||number||


**响应示例**:
```json
{
	"code": 0,
	"msg": "",
	"data": 0
}
```


## 5.获取实时K线数据


**接口地址**: `/spot/open-api/v1/k-line/{symbol}/{interval}`


**请求方式**: <code class="method_get" style="">GET</code>


**请求数据类型**: `application/x-www-form-urlencoded`


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
|data||object||


**响应示例**:
```json
{
	"code": 0,
	"msg": "",
	"data": {}
}
```


## 6.获取交易对最新交易信息


**接口地址**: `/spot/open-api/v1/exchange/{symbol}/recent-trades`


**请求方式**: <code class="method_get" style="">GET</code>


**请求数据类型**: `application/x-www-form-urlencoded`


**响应数据类型**: `application/json`


**接口描述**:


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|symbol|交易对, 格式：BTC-USDT|path|true|string||
|count|交易记录数,最大100|query|true|integer(int32)||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK| |


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code||integer(int32)|integer(int32)|
|msg||string||
|data||number||


**响应示例**:
```json
{
	"code": 0,
	"msg": "",
	"data": 0
}
```


## 7.获取实时盘口数据


**接口地址**: `/spot/open-api/v1/exchange/{symbol}/partial`


**请求方式**: <code class="method_get" style="">GET</code>


**请求数据类型**: `application/x-www-form-urlencoded`


**响应数据类型**: `application/json`


**接口描述**:


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|symbol|交易对, 格式：BTC-USDT|path|true|string||
|depth|盘口的档数,买盘和卖盘分别计算|query|true|integer(int32)||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK| |


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code||integer(int32)|integer(int32)|
|msg||string||
|data||number||


**响应示例**:
```json
{
	"code": 0,
	"msg": "",
	"data": 0
}
```
