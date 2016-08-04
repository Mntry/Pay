# Monetary Pay API
## Credit Sale

###URL
`POST` /credit/sale

###Request Fields (**bold** fields required)
| Field                         | Type    | Length  | Example       | Description                   |
|-------------------------------|---------|-----|-------------------|-------------------------------|
| **Account** <sup>1</sup>      | Numeric | 19  | 4242424242424242  | Account Number                |
| **Expiration** <sup>1</sup>   | String  | 4   | 1220              | Expiration Date (MMYY)        |
| CVV <sup>1</sup>              | String  | 4   | 1234              | Account CVV                   |
| Zip <sup>1</sup>              | String  | 5   | 1234              | Cardholder Zip Code           |
| **Track2** <sup>2</sup>       | String  | 40  | trk               | Card Track2 (stripe)          |
| **Token** <sup>3</sup>        | String  | 20  | otu_123456789     | Monetary Token                |
| **Purchase**                  | String  | 20  | 1.00              | Purchase Amount               |
| Gratuity                      | String  | 20  | 1.00              | Gratuity Amount               |
| Tax                           | String  | 20  | 0.05              | Tax Amount                    |
| InvoiceNo                     | String  | 10  | 1234567890        | Unique Transaction Identifier |

<sup>1</sup> Include these parameters for manually entered account information.<br />
<sup>2</sup> Include this parameter for swiped account information.<br />
<sup>3</sup> Include this parameter for tokenized card information.

###Response Fields
| Field         | Type    | Length  | Example       | Description                           |
|---------------|---------|-----|-------------------|---------------------------------------|
| Status        | String  | 10  | Approved          | Transaction Status                    |
| Account       | Numeric | 19  | XXXXXXXXXXXX4242  | Masked Account Number                 |
| Expiration    | String  | 4   | XXXX              | Masked Expiration Date                |
| Purchase      | String  | 20  | 1.00              | Purchase Amount                       |
| Gratuity      | String  | 20  | 1.00              | Gratuity Amount                       |
| Tax           | String  | 20  | 0.05              | Tax Amount                            |
| InvoiceNo     | String  | 10  | 1234567890        | Echoed Unique Transaction Identifier  |
