### Wallet Transactions

> Sample Resonse

```json
{
    "code": 0,
    "data": {
        "data": [
            {
                "time":      1574640000000,
                "asset":     "BTC",
                "amount":    "-0.129",
                "txType":    "Takeover",
                "status":    "SUCCESS",
                "requestId": "09naslvPvsSLxl9A"
            }
        ],
        "hasNext": false,
        "page": 1,
        "pageSize": 10
    }
}
```

#### Permissions 

You need view permission to access this API.

#### HTTP Request

`GET /api/pro/v1/futures/tx-history`

#### Signature

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-a-request) section.

#### Prehash String

`<timestamp>+futures/tx-history`

#### Response

This API returns paginated data. 

Name            | Type     | Description
--------------- | -------- | -------------- 
**time**        | `Long`   | 


#### Code Sample

Please refer to python code to [get open orders](https://github.com/???/query_order.py)
