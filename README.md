# Monetary Pay API
###Authorization

  Header: `Authorization: [Secret Key Goes Here]`
  
###Content Types
* `application/json`
* `application/xml`
* `x-www-url-encoded`

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
