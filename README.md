# Monetary Pay API
###Authorization

  Header: `Authorization: [Secret Key Goes Here]`
  
###Content Types
* `application/json`
* `application/xml`
* `x-www-url-encoded`

###[Credit Transactions](../blob/master/CREDIT.md)
* Sale `/credit/sale`
* Void Sale `/credit/sale/:id/void`
* Return `/credit/return`
* Void Return `/credit/return/:id/void`
* Auth Only: `/credit/authonly`

###Success Responses
* ```200 OK``` Approved Transaction
* ```402 PAYMENT REQUIRED``` Declined Transaction

###Failure Responses
* ```401 UNAUTHORIZED``` Unauthorized Transaction
* ```404 NOT FOUND``` Resource Not Found

###Example Request

```
POST https://pay.monetary.co/v1/credit/return

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
  "Account": "XXXXXXXXXXXX4242",
  "Expiration": "XXXX",
  "Brand": "VISA",
  "RefNo": "123"
}
```
