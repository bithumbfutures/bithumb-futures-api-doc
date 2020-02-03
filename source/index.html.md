---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - java

toc_footers:
  - <a href='bfutures.io'>Bithumb Futures</a>

includes:
  - futures_rest

  - futures_rest_pub
  - futures_rest_pub_collaterals
  - futures_rest_pub_contracts
  - futures_rest_pub_ref_px
  - futures_rest_pub_market_data
  - futures_rest_pub_funding_rates
    
  - futures_rest_prv
  - futures_rest_prv_account

  - futures_rest_prv_position_collateral
  - futures_rest_prv_position_contract
  - futures_rest_prv_position_risk
  - futures_rest_prv_funding_payment_hist

  - futures_rest_order
  - futures_rest_order_new
  - futures_rest_order_cancel
  - futures_rest_order_open
  - futures_rest_order_hist

  - futures_ws
  - futures_ws_keep_alive
  - futures_ws_sub
  - futures_ws_sub_bar
  - futures_ws_sub_level1
  - futures_ws_sub_level2
  - futures_ws_sub_market_data

  - futures_ws_sub_order
  - futures_ws_sub_order_order
  - futures_ws_sub_order_futures_position
  - futures_ws_sub_order_futures_collateral
  - futures_ws_sub_order_futures_risk

  - futures_ws_req
  - futures_ws_req_level2
  - futures_ws_req_risk
  - futures_ws_req_order_new
  - futures_ws_req_order_cancel
  - futures_ws_req_order_cancel_all

search: true
---


# Bithumb Futures API Documentation

## Using Bithumb Futures API 

The Bithumb Futures API is based on RESTful and WebSocket. 


* The base URL for the RESTful API is `https://bfutures.io/`. 
* The URL for the WebSocket is: `https://bfutures.io/<account-group>/api/v1/stream`. You will have to substitute `<account-group>` with your account group. 

The RESTful API has JSON-encoded responses. All websocket messages are JSON-encoded. 


## Terminology 

### Asset / Collateral Asset 

**collateral asset** refers to the cryptocurrency held in the account. Each collateral asset is uniquely identified by
an `asset` code. For instance, Bitcoin is one collateral asset and has asset code `BTC`. 


### Symbol / Futures Contract

**Futures contract** are tradable products listed on the exchange. Each futures contract is uniquely identified by a `symbol`. 
For instance, the symbol of the BTC perpetrual contract is `BTC-PERP`.


## Making REST API Calls

The RESTful APIs will always repond with JSON objects. 






## Authenticate a RESTful Request 


### Create Request 

To access private data via RESTful APIs, you must include the following headers:

* `x-auth-key` - required, the api key as a string. 
* `x-auth-timestamp` - required, the UTC timestamp in milliseconds of your request
* `x-auth-signature` - required, the request signature (see [Sign a Request](#sign-a-request))

The timestamp in the header will be checked against server time. If the difference is greater than 30 seconds, the request will 
be rejected. 


### Sign a Request

> Signing a RESTful Request

```shell
# bash 
APIPATH=user/info
APIKEY=CEcrjGyipqt0OflgdQQSRGdrDXdDUY2x
SECRET=hV8FgjyJtpvVeAcMAgzgAFQCN36wmbWuN7o3WPcYcYhFd8qvE43gzFGVsFcCqMNk
TIMESTAMP=`date +%s%N | cut -c -13` # 1562952827927
MESSAGE=$TIMESTAMP+$APIPATH
SIGNATURE=`echo -n $MESSAGE | openssl dgst -sha256 -hmac $SECRET -binary | base64`
echo $SIGNATURE  # vBZf8OQuiTJIVbNpNHGY3zcUsK5gJpwb5lgCgarpxYI=

curl -X GET -i \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  -H "x-auth-key: $APIKEY" \
  -H "x-auth-signature: $SIGNATURE" \
  -H "x-auth-timestamp: $TIMESTAMP" \
  https://bfutures.io/api/pro/v1/info
```

```python
# python 3.6+
import time, hmac, hashlib, base64

api_path  = "user/info"
api_key   = "CEcrjGyipqt0OflgdQQSRGdrDXdDUY2x"
sec_key   = "hV8FgjyJtpvVeAcMAgzgAFQCN36wmbWuN7o3WPcYcYhFd8qvE43gzFGVsFcCqMNk"
timestamp = int(round(time.time() * 1e3)) # 1562952827927

message = bytes(f"{timestamp}+{api_path}", 'utf-8')
secret = bytes(sec_key, 'utf-8')

signature = base64.b64encode(hmac.new(secret, message, digestmod=hashlib.sha256).digest())

header = {
  "x-auth-key": api_key,
  "x-auth-signature": signature, 
  "x-auth-timestamp": timestamp,
}
print(signature)  # b'vBZf8OQuiTJIVbNpNHGY3zcUsK5gJpwb5lgCgarpxYI='
```

```java
// java 1.8+
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Base64;

public class SignatureExample {

  public static void main(String[] args) {
    try {
      long timestamp = System.currentTimeMillis(); // 1562952827927
      String api_path = "user/info";
      String secret = "hV8FgjyJtpvVeAcMAgzgAFQCN36wmbWuN7o3WPcYcYhFd8qvE43gzFGVsFcCqMNk";
      String message = timestamp + "+" + api_path;

      Mac sha256_HMAC = Mac.getInstance("HmacSHA256");
      SecretKeySpec secret_key = new SecretKeySpec(secret.getBytes(), "HmacSHA256");
      sha256_HMAC.init(secret_key);

      String hash = Base64.encodeBase64String(sha256_HMAC.doFinal(message.getBytes()));
      System.out.println(hash); // vBZf8OQuiTJIVbNpNHGY3zcUsK5gJpwb5lgCgarpxYI=
    }
    catch (Exception e) {
      System.out.println("Error");
    }
  }
}
```

To query APIs with private data, you must include a signature using base64 encoded HMAC sha256 algorithm. The prehash string is `<timestamp>+<api-path>`. 
The `timestamp` is the UTC timestamp in milliseconds.  


See the code demos in (`bash`/`python`/`java`) on the right.

