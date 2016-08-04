# Monetary Pay API
###Authorization

  Header: `Authorization: secretKEYGOESHERE`
  
###Content Types
* `application/json`
* `application/xml`
* `x-www-url-encoded`

###[Credit Transactions](../master/CREDIT.md)
* Sale `POST /credit/sale`
* Void Sale `POST /credit/sale/:RefNo/void`
* Adjust `PUT /credit/sale/:RefNo`
* Return `POST /credit/return`
* Void Return `POST /credit/return/:RefNo/void`
* Auth Only: `POST /credit/authonly`

###Success Responses
* ```200 OK``` Approved Transaction
* ```402 PAYMENT REQUIRED``` Declined Transaction

###Failure Responses
* ```400 BAD REQUEST``` Invalid Transaction Request
* ```401 UNAUTHORIZED``` Unauthorized Transaction
* ```404 NOT FOUND``` Resource Not Found

###Example Request

```
POST https://pay.monetary.co/v1/credit/sale

Authorization: secretKEYGOESHERE
Content-Type: application/json
Accept: application/json

{
  "Purchase": "1.00",
  "Account": "4242424242424242",
  "Expiration": "1220"
}
```

###Example Response
```
200 OK

{
  "Status": "Approved",
  "Description": "APPROVAL",
  "Account": "XXXXXXXXXXXX4242",
  "Expiration": "XXXX",
  "Brand": "VISA",
  "RefNo": "123",
  "Token": "card_1ABVDEFG2"
}
```
