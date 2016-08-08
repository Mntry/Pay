# Monetary Pay API

### Credit Transaction Requests
* [Sale](#sale)
* [Void Sale](#void-sale)
* [Adjust](#adjust)
* [Return](#return)
* [Void Return](#void-return)
* [Auth Only](#auth-only)

### Credit Transaction Responses
* [Response Fields](#response-fields)

## Sale

`POST` /credit/sale

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| **Account** <sup>1</sup>      | Numeric | 19  | Card Account Number            | Body |
| **Expiration** <sup>1</sup>   | String  | 4   | Card Expiration Date (MMYY)    | Body |
| CVV <sup>1</sup>              | String  | 4   | Card Account CVV               | Body |
| Zip <sup>1</sup>              | String  | 5   | Cardholder Zip Code            | Body |
| **Track2** <sup>2</sup>       | String  | 37  | Card Track2 Data (stripe)      | Body |
| **Token** <sup>3</sup>        | String  | 20  | Monetary Token                 | Body |
| **Purchase**                  | String  | 8   | Purchase Amount                | Body |
| Tip                           | String  | 8   | Tip Amount                     | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier  | Body |
| AuthCode  <sup>4</sup>        | String  | 16  | Voice Authorization Code       | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this field for swiped account information.<br />
<sup>3</sup> Include this field for tokenized card information.<br />
<sup>4</sup> Include this field for authorizations obtained from the voice authorization center.

<br />
## Void Sale

`POST` /credit/sale/**{RefNo}**/void

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **RefNo**                     | String  | 10  | Transaction RefNo to Void     | URL |
| **Token**                     | String  | 20  | Monetary Token                | Body |

<br />
## Adjust

`PUT` /credit/sale/**{RefNo}**

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **RefNo**                     | String  | 10  | Transaction RefNo to Void     | URL  |
| **Token**                     | String  | 20  | Monetary Token                | Body |
| **Purchase** <sup>1</sup>     | String  | 8   | Updated Purchase Amount       | Body |
| **Tip** <sup>1</sup>          | String  | 8   | New or Updated Tip Amount     | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |

<sup>1</sup> Include either or both of these fields.

<br />
## Return

`POST` /credit/return

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **Account** <sup>1</sup>      | Numeric | 19  | Card Account Number           | Body |
| **Expiration** <sup>1</sup>   | String  | 4   | Card Expiration Date (MMYY)   | Body |
| CVV <sup>1</sup>              | String  | 4   | Card Account CVV              | Body |
| Zip <sup>1</sup>              | String  | 5   | Cardholder Zip Code           | Body |
| **Track2** <sup>2</sup>       | String  | 37  | Card Track2 Data (stripe)     | Body |
| **Token** <sup>3</sup>        | String  | 20  | Monetary Token                | Body |
| **Purchase**                  | String  | 8   | Purchase Amount               | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this field for swiped account information.<br />
<sup>3</sup> Include this field for tokenized card information.

<br />
## Void Return

`POST` /credit/return/**{RefNo}**/void

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **RefNo**                     | String  | 10  | Transaction RefNo to Void     | URL  |
| **Token**                     | String  | 20  | Monetary Token                | Body |

<br />
## Auth Only

`POST` /credit/authonly

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **Account** <sup>1</sup>      | Numeric | 19  | Card Account Number           | Body |
| **Expiration** <sup>1</sup>   | String  | 4   | Card Expiration Date (MMYY)   | Body |
| CVV <sup>1</sup>              | String  | 4   | Card Account CVV              | Body |
| Zip <sup>1</sup>              | String  | 5   | Cardholder Zip Code           | Body |
| **Track2** <sup>2</sup>       | String  | 37  | Card Track2 Data (stripe)     | Body |
| **Token** <sup>3</sup>        | String  | 20  | Monetary Token                | Body |
| **Purchase** <sup>4</sup>     | String  | 8   | Purchase Amount               | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier | Body |
| AuthCode  <sup>5</sup>        | String  | 16  | Voice Authorization Code      | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this field for swiped account information.<br />
<sup>3</sup> Include this field for tokenized card information.<br />
<sup>4</sup> `Purchase` value may be `0.00` for a zero-dollar (card verification) authorization.<br />
<sup>5</sup> Include this field for authorizations obtained from the voice authorization center.

<br />
## Responses

Credit transaction response bodies will include the following fields:

###Response Fields
| Field         | Type    | Max Length  | Description                   |
|---------------|---------|-----|---------------------------------------|
| Status <sup>1</sup>        | String  | 10  | Transaction Status                    |
| Account       | Numeric | 19  | Masked Card Account Number            |
| Expiration    | String  | 4   | Masked Card Expiration Date           |
| Brand <sup>2</sup>         | String  | 4   | Card Brand                            |
| Purchase      | String  | 8   | Purchase Amount                       |
| Tip           | String  | 8   | Tip Amount                            |
| Authorized    | String  | 8   | Amount Authorized                     |
| InvoiceNo     | String  | 10  | Echoed Unique Transaction Identifier  |
| RefNo <sup>3</sup>        | String  | 10  | Transaction Reference Number          |

<sup>1</sup> `Status` values: `Approved`, `Declined`, `Success`, or `Error`<br />
<sup>2</sup> `Brand` values: `VISA`, `M/C`, `DCVR`, `AMEX`, `DCLB`, `JCB`, or `OTHER`<br />
<sup>3</sup> Store `RefNo` value for follow-up transaction use.
