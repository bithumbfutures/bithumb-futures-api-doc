### Transactions History 

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

#### HTTP Parameters 

   Name      | Type   | Required | Value Range                    | Description
------------ | ------ | -------- | ------------------------------ |---------------
**page**     | `Int`  | No       | page number, starting from 1   | 
**pageSize** | `Int`  | No       | page size, must be positive    | 


#### Response

This API returns paginated data. 

Name            | Type     | Description
--------------- | -------- | -------------- 
**time**        | `Long`   | UTC timestamp in milliseconds
**asset**       | `String` | asset code, e.g. `BTC`
**amount**      | `String` | changed amount 
**txType**      | `String` | transaction type, such as PositionInjection, Takeover, etc
**status**      | `String` | SUCCESS / FAIED
**requestId**   | `String` | A unique identifier for this balance change event     

Currently, there are four possible values for **status**:

* `Takeover`
* `CollateralConversion`
* `PositionInjection`
* `PositionInjectionBLP`


#### Code Sample

Please refer to python code to [get open orders](https://github.com/bithumbfutures/bithumb-futures-api-demo/blob/master/python/query-futures-tx-history.py)

