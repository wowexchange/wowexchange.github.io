
# Open-API

[中文文档](./README_zh.html),  [English API doc](./)

## 1. General instructions

The interfaces listed in this document, unless explicitly stated, require login to access them. Please contact us to issue a token for access  

The connection information is as follows: 
Host: `https://wowexchange.xyz/gateway-api`

Verification method: 
The verification information is stored in the request headerThe name (key) is' token ', and the value is the obtained token.  
CURL reference: 
```Sh
Curl - X GET - H "Accept: */*" - H "token: S0N... 6AJ" "https://wowexchange.xyz/gateway-api/spot/open-api/v1/wallets"
```

Response result description:   
After the request is successful, the return structure is as follows:

```JavaScript
{
    "code": 200,  //Response business code, 200 indicates success
    "msg": "",    //Error message, non error case is ""
    "data": 0     //Business results, which vary depending on the requestPlease refer to the instructions for each interface for details
}
```

Special instructions:   
Large numbers and floating-point numbers are passed as strings in the returned JSON to avoid losing precision during the transfer process


## 2. Spot order interface


**Interface Address** : `/spot/open-api/v1/exchange/order`


**Request Method** :<code class="method_post">POST</code>


**Request data Type** : `application/json`


**Response Content-Type** : `application/json`


**Interface Description** : 


The reason for the error in the 'msg' field when the order fails for the spot order interface.  
The 'type' field is an order type, allowing 2 values
- 0: Market price
- 1: Price limit


**Request Example** : 


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


**Request Parameters** : 


|Parameter Name | Parameter Description | Request Type | Required | data Type | Schema|
|-------- | -------- | -------- | -------- | -------- | --------|
|OrderRequestDTO | Order request parameters | body | true ||
|&emsp;&emsp; type | Order type, available values: 0: Market price; 1: Limit price | | true | int||
|&emsp;&emsp; amount | Total purchase or sale amount | | true | number||
|&emsp;&emsp; symbol | Symbol,Format: BTC-USDT | | true | string||
|&emsp;&emsp; direction | Order direction, available values: 0: buy; 1: Sell | | true | int||
|&emsp;&emsp; price | price | true | number||
|&emsp;&emsp; useDiscount | Whether to use a discount, available values: 0: Not used; 1: Use | | true | int||


**Response Status** : 


|Status code | Description | Schema|
|-------- |--------|--------|
|200 | OK ||


**Response parameters** : 


|Parameter Name|Parameter Description|Type| Schema|
|--------|--------|--------|--------|
|code | | int | int|
|msg | | string||
|data | Order ID | string||


**Response Example** : 
```json
{
"code": 200, 
"msg": "", 
"data": "5j7bsi....."
}
```


## 3. Obtain wallet account list


**Interface Address** : `/spot/open-api/v1/wallets`


**Request Method** :<code class="method_get">GET</code>


**Response Content-Type** : `application/json`


**Interface Description** : 


Obtain all wallet information for the current user


**Request Parameters** : 


unavailable


**Response Status** : 


|Status code | Description | Schema|
|-------- | --------|--------|
|200 | OK||


**Response parameters** : 


|Parameter Name | Parameter Description | Type | Schema|
|--------|--------|--------|--------|
|code | | int | int|
|msg | | string||
|data | array ||
|&emsp;&emsp; id | ID | string||
|&emsp;&emsp; userId | userID | string||
|&emsp;&emsp; coin | currency | string||
|&emsp;&emsp; coinId | Currency | string||
|&emsp;&emsp; freeAmount | Available quantity | number||
|&emsp;&emsp; freezeAmount | Frozen quantity | number||
|&emsp;&emsp; status | Account status: activate active, freeze free | string||
|&emsp;&emsp; freeUSDTAmount | Number of USDTs with equal freeAmount | number||
|&emsp;&emsp; freezeUSDTAmount | Number of USDTs with equal freezeAmount | number||
|&emsp;&emsp; coinLogo | Currency icon address | string||
|&emsp;&emsp; coinDecimal | Currency precision | int||



**Response Example** : 
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


## 4. Obtain the latest price for symbol


**Interface Address** : `/spot/open-api/v1/last-price/{symbol}`


**Request Method** :<code class="method_get">GET</code>


**Response Content-Type** : `application/json`


**Interface Description** : 


Obtain the real-time price of the specified Symbol, and the response 'data' of this interface is the latest price


**Request Parameters** : 


|Parameter Name | Parameter Description | Request Type | Required | data Type | Schema|
|-------- | -------- | -------- | -------- | -------- | --------|
|Symbol | Symbol, format: BTC-USDT | path | true | string||


**Response Status** : 


|Status code | Description | Schema|
|-------- | --------|--------|
|200 | OK||


**Response parameters** : 


|Parameter Name | Parameter Description | Type | Schema|
|--------|--------|--------|--------|
|code | | int | int|
|msg | | string||
|data | Current price of the sybmol | number||


**Response Example** : 
```json
{
    "code": 200, 
    "msg": "", 
    "data": "3968.2"
}
```


## 5. Obtain real-time K-line data


**Interface Address** : `/spot/open-api/v1/k-line/{symbol}/{interval}`


**Request Method** :<code class="method_get">GET</code>


**Response Content-Type** : `application/json`


**Interface Description** : 


**Request Parameters** : 


|Parameter Name | Parameter Description | Request Type | Required | data Type | Schema|
|-------- | -------- | -------- | -------- | -------- | --------|
|symbol | Symbol, format: BTC-USDT | path | true | string||
|interval | K-line interval, available: M1, M5, M15, M30, H1, H4, D1, W1, MON1 | path | true | string||


**Response Status** : 


|Status code | Description | Schema|
|-------- | --------|--------|
|200 | OK ||


**Response parameters** : 


|Parameter Name | Parameter Description | Type | Schema|
|--------|--------|--------|--------|
|code | | int | int|
|msg | | string||
|data||object| |
|&emsp;&emsp;s|Symbol|string||
|&emsp;&emsp;i|Interval|string||
|&emsp;&emsp;dd||object| |
|&emsp;&emsp;&emsp;&emsp;o|opening price|string||
|&emsp;&emsp;&emsp;&emsp;h|highest price|string||
|&emsp;&emsp;&emsp;&emsp;l|lowest price|string||
|&emsp;&emsp;&emsp;&emsp;c|closing price|string||
|&emsp;&emsp;&emsp;&emsp;h24|highest price of 24h|string||
|&emsp;&emsp;&emsp;&emsp;l24|lowest price of 24h|string||
|&emsp;&emsp;&emsp;&emsp;v24|Symbol left volume in the past 24 hours|string||
|&emsp;&emsp;&emsp;&emsp;vv24|Symbol right volume in the past 24 hours|string||
|&emsp;&emsp;&emsp;&emsp;p24|24-hour price change ratio|string||
|&emsp;&emsp;&emsp;&emsp;cp|24-hour price fluctuation volume|string||
|&emsp;&emsp;&emsp;&emsp;v|Volume|string||
|&emsp;&emsp;&emsp;&emsp;vv|Turnover|string||
|&emsp;&emsp;&emsp;&emsp;pt|time|integer||
|&emsp;&emsp;&emsp;&emsp;sse|There is no need to care about this value for K-line|string||
|&emsp;&emsp;&emsp;&emsp;sos|There is no need to care about this value for K-line|string||


**Response Example** : 
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






## 6. Get Historical K-Line


**Interface Address**:`/gateway-api/spot/open-api/v1/k-line/history/{symbol}/{interval}`


**Request Method** :<code class="method_get">GET</code>


**Response Content-Type** : `application/json`


**Interface Description** : 



**Request Parameters** : 

|Parameter Name | Parameter Description | Request Type | Required | data Type | Schema|
| -------- | -------- | ----- | -------- | -------- | ------ |
|symbol | Symbol, format: BTC-USDT | path | true | string||
|interval | K-line interval, available: M1, M5, M15, M30, H1, H4, D1, W1, MON1 | path | true | string||
|endTime|Time of last data, in seconds (results do not include this time data)|query|true|long||
|limit|Returns the number of records, default 100|query|true|int||


**Response Status** : 


|Status code | Description | Schema|
| -------- | -------- | ----- | 
|200|OK| |


**Response parameters** : 


|Parameter Name | Parameter Description | Type | Schema|
| -------- | -------- | ----- |----- | 
|code||int|int|
|msg||string||
|data||object| |
|&emsp;&emsp;klines|K-Line Historical Data|array| |
|&emsp;&emsp;&emsp;&emsp;close|closing price|number||
|&emsp;&emsp;&emsp;&emsp;high|highest price|number||
|&emsp;&emsp;&emsp;&emsp;low|lowest price|number||
|&emsp;&emsp;&emsp;&emsp;open|opening price|number||
|&emsp;&emsp;&emsp;&emsp;time|k-line time in milliseconds|string||
|&emsp;&emsp;&emsp;&emsp;volume|symbol left volume|number||
|&emsp;&emsp;&emsp;&emsp;vvolume|symbol right volume|number||


**Response Example** :  
```javascript
{
    "code": 0,
    "msg": "",
    "data": {
        "klines": [
            {
                "close": 0,
                "high": 0,
                "low": 0,
                "open": 0,
                "time": "",
                "volume": 0,
                "vvolume": 0
            }
        ]
    }
}
```








## 7. Obtain the latest transaction information for transaction pairs

**Interface Address** : `/spot/open-api/v1/exchange/{symbol}/recent-trades`

**Request Method** :<code class="method_get">GET</code>

**Response Content-Type** : `application/json`

**Interface Description** : 

**Request Parameters** : 

|Parameter Name | Parameter Description | Request Type | Required | data Type | Schema|
|-------- | -------- | -------- | -------- | -------- | --------|
|symbol | Symbol, format: BTC-USDT | path | true | string||
|count | Number of transaction records, maximum 100 | query | true | int||


**Response Status** : 


|Status code | Description | Schema|
|-------- | --------|--------|
|200 | OK ||


**Response parameters** : 


|Parameter Name | Parameter Description | Type | Schema|
|--------|--------|--------|--------|
|code | | int | int|
|msg | | string||
|data | | object ||
|&emsp;&emsp; s | Symbol | string||
|&emsp;&emsp; ps | Number of records | int||
|&emsp;&emsp; i | Transaction record list | array ||
|&emsp;&emsp;&emsp;&emsp; a | Quantity | number||
|&emsp;&emsp;&emsp;&emsp; p | Price | number||
|&emsp;&emsp;&emsp;&emsp; d | Trading direction, 0: buy, 1: sell | int||
|&emsp;&emsp;&emsp;&emsp; t | Transaction closing time | long||


**Response Example** : 
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


## 8. Obtain real-time partial


**Interface Address** : `/spot/open-api/v1/exchange/{symbol}/partial`


**Request Method** :<code class="method_get">GET</code>

**Response Content-Type** : `application/json`

**Interface Description** : 

Obtain buy and sell data for a specified Symbol, with a maximum number of 'depth' records returned for each pair, and a maximum of 20 records

**Request Parameters** : 

|Parameter Name | Parameter Description | Request Type | Required | data Type | Schema|
|-------- | -------- | -------- | -------- | -------- | --------|
|symbol | Symbol, format: BTC-USDT | path | true | string||
|depth | The number of slots in the opening, calculated separately for buying and selling, with a maximum of 20 | query | true | int||


**Response Status** : 


|Status code | Description | Schema|
|-------- | --------| --------|
|200 | OK ||


**Response parameters** : 


|Parameter Name | Parameter Description | Type | Schema|
|--------| --------| --------| --------|
|code | | int | int|
|msg | | string||
|data | | object ||
|&emsp;&emsp; s | Symbol | string||
|&emsp;&emsp; a | Sell | array ||
|&emsp;&emsp;&emsp;&emsp; p | Price | number||
|&emsp;&emsp;&emsp;&emsp; a | Quantity | number||
|&emsp;&emsp;&emsp;&emsp; t | total amount | number||
|&emsp;&emsp; b | Buy |array|
|&emsp;&emsp;&emsp;&emsp; p | Price | number||
|&emsp;&emsp;&emsp;&emsp; a | Quantity | number||
|&emsp;&emsp;&emsp;&emsp; t | total amount | number||

**Response Example** : 

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







## 9. Paging to get a list of orders in progress


**Interface Address**: `/spot/open-api/v1/exchange/orders`


**Request Method** : <code class="method_get">GET</code>


**Response Content-Type**: `application/json`


**Interface Description**:

This interface does not return the `detail` field value.

**Request Parameters** : 

|Parameter Name | Parameter Description | Request Type | Required | data Type | Schema|
| -------- | -------- | ----- | -------- | -------- | ------ |
|status|Order Status, 0:Transaction in progress; 1:Completed|query|true|int||
|page|Page number, from 0|query|false|int||
|pageSize|Records per page|query|false|int||


**Response Status** : 


|Status code | Description | Schema|
| -------- | -------- | ----- | 
|200|OK| |



**Response parameters** : 


|Parameter Name | Parameter Description | Type | Schema|
| -------- | -------- | ----- |----- | 
|code||int|int|
|msg||string||
|data||object||
|&emsp;&emsp;count|Number of records|int||
|&emsp;&emsp;total|Total number of records|long||
|&emsp;&emsp;page|Page number, from 0|int||
|&emsp;&emsp;pageSize|Records per page|int||
|&emsp;&emsp;list||array| |
|&emsp;&emsp;&emsp;orderId|Order ID|string||
|&emsp;&emsp;&emsp;memberId|User ID|integer||
|&emsp;&emsp;&emsp;type|Order type, available:MARKET_PRICE,LIMIT_PRICE|string||
|&emsp;&emsp;&emsp;amount|amount|number||
|&emsp;&emsp;&emsp;symbol|symbol|string||
|&emsp;&emsp;&emsp;tradedAmount|Amount of transactions completed|number||
|&emsp;&emsp;&emsp;turnover|total amount|number||
|&emsp;&emsp;&emsp;coinSymbol|token|string||
|&emsp;&emsp;&emsp;baseSymbol|base token|string||
|&emsp;&emsp;&emsp;status|Order status, available:TRADING,COMPLETED,CANCELED,OVERTIMED|string||
|&emsp;&emsp;&emsp;direction|Order direction, available:BUY,SELL|string||
|&emsp;&emsp;&emsp;price|price|number||
|&emsp;&emsp;&emsp;time|Time to order|integer||
|&emsp;&emsp;&emsp;completedTime|Completion time|integer||
|&emsp;&emsp;&emsp;canceledTime|Cancellation time|integer||
|&emsp;&emsp;&emsp;useDiscount|discount|string||
|&emsp;&emsp;&emsp;detail|Transacted List|array||
|&emsp;&emsp;&emsp;completed|Whether to complete, true: complete, false: other cases|boolean||


**Response Example** : 

```javascript
{
    "code": 0,
    "msg": "",
    "data": {
        "count": 0,
        "total": 0,
        "page": 0,
        "pageSize": 0,
        "list": [
            {
                "orderId": "",
                "memberId": 0,
                "type": "",
                "amount": 0,
                "symbol": "",
                "tradedAmount": 0,
                "turnover": 0,
                "coinSymbol": "",
                "baseSymbol": "",
                "status": "",
                "direction": "",
                "price": 0,
                "time": 0,
                "completedTime": 0,
                "canceledTime": 0,
                "useDiscount": "",
                "detail": null,
                "completed": true
            }
        ]
    }
}
```


## 10. Get order information based on order ID


**Interface Address**: `/spot/open-api/v1/exchange/order/{orderId}`


**Request Method** : <code class="method_get">GET</code>


**Response Content-Type**: `application/json`


**Interface Description**:

This interface response contains the `detail` list

**Request Parameters** : 

|Parameter Name | Parameter Description | Request Type | Required | data Type | Schema|
| -------- | -------- | ----- | -------- | -------- | ------ |
|orderId|Order ID|path|true|string||


**Response Status** : 


|Status code | Description | Schema|
| -------- | -------- | ----- | 
|200|OK| |



**Response parameters** : 


|Parameter Name | Parameter Description | Type | Schema|
| -------- | -------- | ----- |----- | 
|code||int|int|
|msg||string||
|data|| object | |
|&emsp;&emsp;&emsp;orderId|Order ID|string||
|&emsp;&emsp;&emsp;memberId|User ID|integer||
|&emsp;&emsp;&emsp;type|Order type, available:MARKET_PRICE,LIMIT_PRICE|string||
|&emsp;&emsp;&emsp;amount|amount|number||
|&emsp;&emsp;&emsp;symbol|symbol|string||
|&emsp;&emsp;&emsp;tradedAmount|Amount of transactions completed|number||
|&emsp;&emsp;&emsp;turnover|total amount|number||
|&emsp;&emsp;&emsp;coinSymbol|token|string||
|&emsp;&emsp;&emsp;baseSymbol|base token|string||
|&emsp;&emsp;&emsp;status|Order status, available:TRADING,COMPLETED,CANCELED,OVERTIMED|string||
|&emsp;&emsp;&emsp;direction|Order direction, available:BUY,SELL|string||
|&emsp;&emsp;&emsp;price|price|number||
|&emsp;&emsp;&emsp;time|Time to order|integer||
|&emsp;&emsp;&emsp;completedTime|Completion time|integer||
|&emsp;&emsp;&emsp;canceledTime|Cancellation time|integer||
|&emsp;&emsp;&emsp;useDiscount|discount|string||
|&emsp;&emsp;&emsp;detail|Transacted List|array||
|&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;id|Transaction ID|integer||
|&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;orderId|Order ID|string||
|&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;price|price|number||
|&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;amount|amount|number||
|&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;turnover|turnover|number||
|&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;fee|fee|number||
|&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;time|Date of transaction|integer||
|&emsp;&emsp;&emsp;completed|Whether to complete, true: complete, false: other cases|boolean||



**Response Example** : 

```javascript
{
    "code": 0,
    "msg": "",
    "data": {
        "orderId": "",
        "memberId": 0,
        "type": "",
        "amount": 0,
        "symbol": "",
        "tradedAmount": 0,
        "turnover": 0,
        "coinSymbol": "",
        "baseSymbol": "",
        "status": "",
        "direction": "",
        "price": 0,
        "time": 0,
        "completedTime": 0,
        "canceledTime": 0,
        "useDiscount": "",
        "detail": [
            {
                "id": 0,
                "orderId": "",
                "price": 0,
                "amount": 0,
                "turnover": 0,
                "fee": 0,
                "time": 0
            }
        ],
        "completed": true
    }
}
```


## 11. Cancel an order


**Interface Address**: `/spot/open-api/v1/exchange/order/{orderId}`


**Request Method**: <code class="method_delete">DELETE</code>


**Response Content-Type**: `application/json`


**Interface Description**:



**Request Parameters** : 

|Parameter Name | Parameter Description | Request Type | Required | data Type | Schema|
| -------- | -------- | ----- | -------- | -------- | ------ |
|orderId|Order ID|path|true|string||


**Response Status** : 


|Status code | Description | Schema|
| -------- | -------- | ----- | 
|200|OK| |



**Response parameters** : 


|Parameter Name | Parameter Description | Type | Schema|
| -------- | -------- | ----- |----- | 
|code||int|int|
|msg||string||
|data|true:Processing success,false:Processing failure|boolean||


**Response Example** : 

```javascript
{
    "code": 0,
    "msg": "",
    "data": true
}
```
