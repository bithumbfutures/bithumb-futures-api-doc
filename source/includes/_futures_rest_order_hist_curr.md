### List Current History Orders

> Current History Orders - Successful Response (Status 200, code 0)

```json
{
    "ac": "FUTURES",
    "accountId": "futZrwfTaL4Py6M05X0SnJ9QFIuj6k2Q",
    "code": 0,
    "data": [
        {
            "seqNum":       168383,
            "symbol":       "BTC-PERP",
            "side":         "Buy",
            "avgPx":        "9825.235",
            "cumFee":       "0.080566927",
            "cumFilledQty": "0.01",
            "errorCode":    "",
            "execInst":     "NULL_VAL",
            "feeAsset":     "USDT",
            "lastExecTime":  1581708299976,
            "orderId":      "r170452951ca5362614103bbtcpcS7p",
            "orderQty":     "0.01",
            "orderType":    "Limit",
            "price":        "9950.5",
            "status":       "Filled",
            "stopPrice":    ""
        }
    ]
}
```

This API returns all current history orders for the account specified. This API will only respond with most recently closed orders cached by the server. 
To query the full history, please use the [**Historical Orders**](#historical-orders) API. 


#### HTTP Request

`GET <account-group>/api/pro/v1/futures/order/hist/current`

#### Signature

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-request) section.

#### Prehash String

`<timestamp>+order/hist/current`


#### Request Parameters

 Name            | Type      | Required | Description                                                                                 
---------------- | --------- | -------- | ------------------------------------------------------------------------------------------- 
**n**             | `Int`     | No       | maximum number of orders to be included in the response
**symbol**        | `String`  | No       | symbol filter, e.g. `"BTC-PERP"`
**executedOnly**  | `Boolean` | No       | if `True`, include orders with non-zero filled quantities only.


#### Response

Return a list of history orders in *"data"* field.

