# Monetary Pay API
## Credit Sale

###URL

  `POST` /credit/sale

###Request Parameters
#####(**bold** parameters required)


| Parameter        | Type           | Length  | Example   |
| ------------- |-------------| -----|------|
| **Account** <sup>1</sup>      | Numeric | 19 | 4242424242424242 |
| **Expiration** <sup>1</sup> | String |    4 | 1220 |
| CVV <sup>1</sup> | String |    4 | 1234 |
| Zip <sup>1</sup> | String |    5 | 1234 |
| **Track2** <sup>2</sup> | String |    40 | trk |
| **Token** <sup>3</sup> | String |    20 | otu_123456789 |
| **Purchase** | String |    20 | 1.00 |
| Gratuity | String |    20 | 1.00 |
| Tax | String |    20 | 0.05 |


  <sup>1</sup> Include these parameters for manually entered account information.<br />
  <sup>2</sup> Include this parameter for swiped account information.<br />
  <sup>3</sup> Include this parameter for tokenized card information.


###Success Responses

####Approved
```json
200 OK

{
  "Status": "Approved",
  "Account": "XXXXXXXXXXXX4242",
  "Expiration": "XXXX",
  "Brand": "VISA",
  "RefNo": "123"
}
```
    
####Declined:
```json
402 PAYMENT REQUIRED

{
  "Status": "Declined",
  "Account": "XXXXXXXXXXXX4242",
  "Expiration": "XXXX",
  "Brand": "VISA",
  "RefNo": "123"
}
```
 
###Failure Responses
```401 UNAUTHORIZED```

```402 PAYMENT REQUIRED```

```404 NOT FOUND```

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
