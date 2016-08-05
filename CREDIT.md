# Monetary Pay API - Credit Transactions

## Sale

###URL
`POST` /credit/sale

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **Account** <sup>1</sup>      | Numeric | 19  | Account Number                | Body |
| **Expiration** <sup>1</sup>   | String  | 4   | Expiration Date (MMYY)        | Body |
| CVV <sup>1</sup>              | String  | 4   | Account CVV                   | Body |
| Zip <sup>1</sup>              | String  | 5   | Cardholder Zip Code           | Body |
| **Track2** <sup>2</sup>       | String  | 37  | Card Track2 Data (stripe)     | Body |
| **Token** <sup>3</sup>        | String  | 20  | Monetary Token                | Body |
| **Purchase**                  | String  | 8   | Purchase Amount               | Body |
| Tip                           | String  | 8   | Tip Amount                    | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this fields for swiped account information.<br />
<sup>3</sup> Include this fields for tokenized card information.

## Void Sale

###URL
`POST` /credit/sale/:RefNo/void

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **RefNo**                     | String  | 10  | Transaction RefNo to Void     | URL:RefNo |
| **Token**                     | String  | 20  | Monetary Token                | Body |


## Responses

Credit transaction response bodies will include the following fields:

###Response Fields
| Field         | Type    | Max Length  | Description                           |
|---------------|---------|-----|---------------------------------------|
| Status        | String  | 10  | Transaction Status                    |
| Account       | Numeric | 19  | Masked Account Number                 |
| Expiration    | String  | 4   | Masked Expiration Date                |
| Brand         | String  | 4   | Card Brand                            |
| Purchase      | String  | 8   | Purchase Amount                       |
| Tip           | String  | 8   | Tip Amount                            |
| Authorized    | String  | 8   | Amount Authorized                     |
| InvoiceNo     | String  | 10  | Echoed Unique Transaction Identifier  |
| RefNo         | String  | 10  | Transaction Reference Number          |
