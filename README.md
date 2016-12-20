# Getting Started with Monetary Pay API
###Authorization

Authorization is easy, just insert your secret key in the `Authorization` header:

`Authorization: secretKEYGOESHERE`
  
###Content Types
Communicate with us in your favorite content type!

We support the following for `Content-Type` and `Accepts` values:

* `application/json`
* `application/xml`
* `x-www-url-encoded`

##Transactions

###[Credit Transactions](CREDIT.md)
* [Supported Transactions](CREDIT.md#supported-transactions) `GET` /credit
* [Sale](CREDIT.md#sale) `POST` /credit/sale
* [Void Sale](CREDIT.md#void-sale) `POST` /credit/sale/**{RefNo}**/void
* [Adjust](CREDIT.md#adjust) `PUT` /credit/sale/**{RefNo}**
* [Return](CREDIT.md#return) `POST` /credit/return
* [Void Return](CREDIT.md#void-return) `POST` /credit/return/**{RefNo}**/void
* [PreAuth](CREDIT.md#preauth) `POST` /credit/preauth
* [Capture](CREDIT.md#capture) `PUT` /credit/preauth/**{RefNo}**
* [Auth Only](CREDIT.md#auth-only) `POST` /credit/authonly

###[Debit Transactions](DEBIT.md)
* [Sale](DEBIT.md#sale) `POST` /debit/sale
* [Return](DEBIT.md#return) `POST` /debit/return

###[Stored Value Transactions](STOREDVALUE.md)
* [Load](STOREDVALUE.md#load) `POST` /storedvalue/load
* [Void Load](STOREDVALUE.md#void-load) `POST` /storedvalue/load/**{RefNo}**/void
* [Sale](STOREDVALUE.md#sale) `POST` /storedvalue/sale
* [Void Sale](STOREDVALUE.md#void-sale) `POST` /storedvalue/sale/**{RefNo}**/void
* [Balance](STOREDVALUE.md#balance) `POST` /storedvalue/balance
* [Create](STOREDVALUE.md#create) `POST` /storedvalue/create
* [Set](STOREDVALUE.md#set) `POST` /storedvalue/set

###Success Responses
* ```200 OK``` Approved Transaction
* ```402 PAYMENT REQUIRED``` Declined Transaction

###Failure Responses
* ```400 BAD REQUEST``` Invalid Transaction Request
* ```401 UNAUTHORIZED``` Unauthorized Transaction
* ```404 NOT FOUND``` Resource Not Found

###Example Credit Sale Request

```
POST https://pay.monetary.co/v1/credit/sale

Authorization: secretKEYGOESHERE
Content-Type: application/json
Accept: application/json

{
  "Amount": "1.00",
  "Account": "4242424242424242",
  "Expiration": "1220"
}
```

###Example Credit Sale Response
```
200 OK

{
  "Status": "Approved",
  "Message": "APPROVAL",
  "Account": "XXXXXXXXXXXX4242",
  "Expiration": "XXXX",
  "Brand": "VISA",
  "AuthCode": "ABC123",
  "RefNo": "123",
  "Amount": "1.00",
  "Authorized": "1.00",
  "Token": "card_1ABCDEFG2"
}
```

##Using Tokens
As you can see in the [example response above](#example-sale-response), every successful transaction response will include a `Token` which you can use in subsequent transactions for that account!

For example, this is how to void the above example sale using the `RefNo` and `Token` it returned:

###Example Credit Void Request with Token

```
POST https://pay.monetary.co/v1/credit/sale/123/void

Authorization: secretKEYGOESHERE
Content-Type: application/json
Accept: application/json

{
  "Token": "card_1ABCDEFG2"
}
```

###Example Credit Void Response with Token
```
200 OK

{
  "Status": "Approved",
  "Message": "APPROVAL",
  "Account": "XXXXXXXXXXXX4242",
  "Expiration": "XXXX",
  "Brand": "VISA",
  "RefNo": "124",
  "Amount": "1.00",
  "Authorized": "1.00",
  "Token": "card_1ABCDEFG2"
}
```
