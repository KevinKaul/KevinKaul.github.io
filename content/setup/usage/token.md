---
title: "- 1. Generate JWT token"
weight: 2
---

> Assume that you already have AppKey and AppSecret, and know the domain name address to request.

## Get Token By API


```shell
curl -X POST 'https://{{$HOST}}/auth/generateToken' \
--header 'Content-Type: application/json' \
--data '{
    "timestamp":{{$timestamp}},
    "signature":{{$signature}},
    "appKey":"{{$appKey}}"
}'
```

e.g.
```json
{
    "timestamp":1690637789,
    "signature":"FEecGK0xbTOF3yxH3zq11FgkqFg=",
    "appKey":"01e93ab5-dcb2-4c6b-a321-02c0c8d3831"
}
// appSecret : 04a013293939f96 
```


### How the signature is constructed

Step 1: Construct a normalized request string stringToSign using the `appKey` and `timestamp` request parameters (note the order of the parameters), such as:
```bash
  appId=XXXX-XXXX-XXXX&timestamp=1690637789
```

Step 2: The request string constructed in the previous step is calculated using the `HMAC-SHA1` signature algorithm to calculate the corresponding  signature (Base64 encoding). Use `appSecret` as the key for the signature algorithm:
```bash
  signature = Base64(HMAC-SHA1(stringToSign, appSecret))
```

#### Generate  signature sample code
- [python](sdk/signature_python.md)

- [golang](sdk/signature_golang.md)

- [java](sdk/signature_java.md)

- [c](sdk/signature_c.md)

- [c#](sdk/signature_cs.md)

### How to use token
- **Recommended** : Put token in the request `header` of websockets

```bash
 "Authorization" : "Bearer {{$TOKEN}}"
```

> This is more in line with the OAuth 2.0 specification, and you can also choose not to carry `Bearer` and directly pass in the token.


- The second way is to directly splice the token directly behind the request address.such as:
```bash
 wss://{{$HOST}}/en-US/sentence?Authorization={{$TOKEN}}
```