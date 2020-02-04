### Wallet Transaction History

> Wallet Transaction History 

```json
{
  "code": 0,
  "data": {
    "data": [
      {
        "asset":                "USDT",
        "requestId":            "cOagK5svg9ookf3cJBidbcdVbnW1daDl",
        "amount":               "119",
        "commission":           "0",
        "destAddress":          {"address": "0x5dc4923bd61bea0f5ecfb0db7de6b137060360bd"},
        "networkTransactionId": "0x473f725ae197ea8e2828700cee7d2c9b2fe50f74c41ba38c2928d5ebfd7400cd",
        "numConfirmations":     20,
        "numConfirmed":         20,
        "status":               "confirmed",
        "time":                 1580657103000,
        "transactionType":      "deposit"
      }
    ],
    "page"    : 1,
    "pageSize": 20,
    "hasNext" : false
  }
}
```

You can obtain history of wallet deposit/withdrawal transactions via this API.

#### Permissions 

You need view permission to access this API.

#### HTTP Request 

`GET /api/pro/wallet/transactions`

You don't need to specify `<account-group>` for this API.

#### Request Parameters

You can specify the following parameters:

 Name        | Type               | Default  | Description
------------ | ------------------ | -------- | --------------------- 
**asset**    | `Optional[Int]`    | Null     | asset code
**page**     | `Optional[Int]`    | 1        | page number, must be greater than 0.
**pageSize** | `Optional[Int]`    | 20       | page size, must be greater than 0.
**startTs**  | `Optional[Long]`   | Time.Min | start of the query range, UTC timestamp in milliseconds
**endTs**    | `Optional[Long]`   | Time.Max | end of the query range, UTC timestamp in milliseconds
**txType**   | `Optional[String]` | Null     | the transaction type filter: `deposit` / `withdrawal`



#### Response Content

The `data` field of the API response contains the paginated historical data. All records are sorted in reverse chronological order.

 Name        | Type           | Description
------------ | -------------- | --------------------- 
**page**     | `Int`          | page number, must be greater than 0.
**pageSize** | `Int`          | page size, must be greater than 0.
**hasNext**  | `Boolean`      | if True, there are more records to show
**data**     | `List[Object]` | a list of transaction records. See below for details

Each transaction record contains the following fields:

 Name                    | Type     | Description
------------------------ | -------- | --------------------- 
**asset**                | `String` | asset code
**requestId**            | `String` | an unique identifier for the transaction
**amount**               | `String` | amount in transaction
**commission**           | `String` | commission charged
**destAddress**          | `Object` | destination address ID, it usually contains an `address` field and an optional `destTag` field
**networkTransactionId** | `String` | the id/hash of the transaction, for transactions among exchange users, this field is "-"
**numConfirmations**     | `Int`    | deposit will be viewd as final after the number of blocks confirmed reaches this value
**numConfirmed**         | `Int`    | currently number of blocks confirmed
**status**               | `String` | reviewing / pending / confirmed / rejected
**time**                 | `Long`   | UTC Timestamp in milliseconds
**transactionType**      | `String` | deposit / withdrawal

