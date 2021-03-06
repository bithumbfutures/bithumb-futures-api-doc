### Ticker 

> Ticker for one product

```json
// curl -X GET 'https://bithumbfutures.com/api/pro/v1/ticker?symbol=BTC-PERP'
{
    "code": 0,
    "data": {
        "symbol": "BTC-PERP",
        "open":   "9000",
        "close":  "9000",
        "high":   "9000",
        "low":    "9000",
        "volume": "1.02",
        "ask": [ "9500", "0.4" ],
        "bid": [ "8500", "0.1" ]
    }
}
```

> List of Tickers for one or multiple products

```json
// curl -X GET "https://bithumbfutures.com/api/pro/v1/ticker?symbol=BTC-PERP,"
{
    "code": 0,
    "data": [
        {
            "symbol": "BTC-PERP",
            "open":   "9000",
            "close":  "9000",
            "high":   "9000",
            "low":    "9000",
            "volume": "1.02",
            "ask": [ "9500", "0.4" ],
            "bid": [ "8500", "0.1" ]
        }
    ]
}
```

**HTTP Request**

`GET api/pro/v1/ticker`

You can get summary statistics of one or multiple symbols with this API. 

#### Request Parameters

Name       | Type      | Required | Value Range | Description
-----------| --------- | -------- | ----------- | ---------------
`symbol`   | `String`  |  No      |             | you may specify one, multiple, or all symbols of interest. See below.


This API endpoint accepts one optional string field `symbol`: 

* If you do not specify `symbol`, the API will responde with tickers of all symbols in a list. 
* If you set `symbol` to be a single symbol, such as `BTC-PERP`, the API will respond with the ticker of the target symbol as an object. 
  If you want to wrap the object in a one-element list, append a comma to the symbol, e.g. `BTC-PERP,`.
* (Not supported yet) You shall specify `symbol` as a comma separated symbol list, e.g. `BTC-PERP,ETH-PERP`. The API will respond with a list of tickers. 

#### Respond Content

The API will respond with a ticker object or a list of ticker objects, depending on how you set the `symbol` parameter. 

Each ticker object contains the following fields:

 Field      | Type                 | Description                                                                                 
----------- | -------------------- | --------------------- 
 `symbol`   |  `String`            | 
 `open`     |  `String`            | the traded price 24 hour ago
 `close`    |  `String`            | the last traded price
 `high`     |  `String`            | the highest price over the past 24 hours 
 `low`      |  `String`            | the lowest price over the past 24 hours 
 `volume`   |  `String`            | the total traded volume in quote asset over the paste 24 hours
 `ask`      |  `[String, String]`  | the price and size at the current best ask level
 `bid`      |  `[String, String]`  | the price and size at the current best bid level

#### Code Sample

Please refer to python code to [query ticker info]{https://github.com/bithumbfutures/bithumb-futures-api-demo/blob/master/python/query-ticker.py}
