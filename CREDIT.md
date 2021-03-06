# Monetary Pay API

### Supported Transactions Request
* [Supported Transactions](#supported-transactions)

### Credit Transaction Requests
* [Sale](#sale)
* [Void Sale](#void-sale)
* [Adjust](#adjust)
* [Return](#return)
* [Void Return](#void-return)
* [PreAuth](#preauth)
* [Capture](#capture)
* [Auth Only](#auth-only)

### Transaction Detail Request
* [Transaction Detail](#transaction-detail)

### Credit Transaction Responses
* [Response Fields](#response-fields)

### Duplicate Checking
* [Duplicate Checking Behavior](#duplicate-checking-1)

## Supported Transactions
Depending on the merchant's processor, a subset of available Monetary transactions may be unavailable. This endpoint will report the processor's supported status of each transaction for the provided merchant secret key.

`GET` /credit

### Supported Transactions Response Fields
| Field                         | Type     |
|-------------------------------|----------|
| Sale                          | Boolean  |
| VoidSale                      | Boolean  |
| PreAuth                       | Boolean  |
| PreAuthCapture                | Boolean  |
| Adjust                        | Boolean  |
| Return                        | Boolean  |
| VoidReturn                    | Boolean  |
| AuthOnly                      | Boolean  |

<br />

## Sale

`POST` /credit/sale

### Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| **Account** <sup>1</sup>      | Numeric | 19  | Card Account Number            | Body |
| **Expiration** <sup>1</sup>   | String  | 4   | Card Expiration Date (MMYY)    | Body |
| CVV <sup>1</sup>              | String  | 4   | Card Account CVV               | Body |
| Zip <sup>1</sup>              | String  | 5   | Cardholder Zip Code            | Body |
| **Track2** <sup>2</sup>       | String  | 37  | Card Track2 Data (stripe)      | Body |
| **Token** <sup>3</sup>        | String  | 20  | Monetary Token                 | Body |
| **AccountKey** <sup>4</sup>   | String  | 20  | Account Encryption Key         | Body |
| **EncryptedAccount** <sup>4</sup>| String | 224 | Encrypted Account Data Block | Body |
| **Amount**                    | String  | 8   | Transaction Amount             | Body |
| Tip                           | String  | 8   | Tip Amount                     | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier  | Body |
| AuthCode  <sup>5</sup>        | String  | 16  | Voice Authorization Code       | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |
| Trace                         | String  | 40  | Echoed in Response             | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this field for swiped account information.<br />
<sup>3</sup> Include this field for tokenized card information.<br />
<sup>4</sup> Include these fields for encrypted account information.<br />
<sup>5</sup> Include this field for authorizations obtained from the voice authorization center.

<br />

## Void Sale

`POST` /credit/sale/**{RefNo}**/void

### Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **RefNo**                     | String  | 19  | Transaction RefNo to Void     | URL |
| **Token**                     | String  | 20  | Monetary Token                | Body |
| Trace                         | String  | 40  | Echoed in Response             | Body |

<br />

## Adjust

`PUT` /credit/sale/**{RefNo}**

### Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **RefNo**                     | String  | 19  | Transaction RefNo to Void     | URL  |
| **Token**                     | String  | 20  | Monetary Token                | Body |
| **Amount** <sup>1</sup>       | String  | 8   | Updated Transaction Amount    | Body |
| **Tip** <sup>1</sup>          | String  | 8   | New or Updated Tip Amount     | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction| Body |
| Trace                         | String  | 40  | Echoed in Response             | Body |

<sup>1</sup> Include either of these fields.
<br />

## Return

`POST` /credit/return

### Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **Account** <sup>1</sup>      | Numeric | 19  | Card Account Number           | Body |
| **Expiration** <sup>1</sup>   | String  | 4   | Card Expiration Date (MMYY)   | Body |
| CVV <sup>1</sup>              | String  | 4   | Card Account CVV              | Body |
| Zip <sup>1</sup>              | String  | 5   | Cardholder Zip Code           | Body |
| **Track2** <sup>2</sup>       | String  | 37  | Card Track2 Data (stripe)     | Body |
| **Token** <sup>3</sup>        | String  | 20  | Monetary Token                | Body |
| **AccountKey** <sup>4</sup>   | String  | 20  | Account Encryption Key         | Body |
| **EncryptedAccount** <sup>4</sup>| String | 224 | Encrypted Account Data Block | Body |
| **Amount**                    | String  | 8   | Transaction Amount            | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |
| Trace                         | String  | 40  | Echoed in Response             | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this field for swiped account information.<br />
<sup>3</sup> Include this field for tokenized card information.<br />
<sup>4</sup> Include these fields for encrypted account information.

<br />

## Void Return

`POST` /credit/return/**{RefNo}**/void

### Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **RefNo**                     | String  | 19  | Transaction RefNo to Void     | URL  |
| **Token**                     | String  | 20  | Monetary Token                | Body |
| Trace                         | String  | 40  | Echoed in Response             | Body |
<br />

## PreAuth

`POST` /credit/preauth

### Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| **Account** <sup>1</sup>      | Numeric | 19  | Card Account Number            | Body |
| **Expiration** <sup>1</sup>   | String  | 4   | Card Expiration Date (MMYY)    | Body |
| CVV <sup>1</sup>              | String  | 4   | Card Account CVV               | Body |
| Zip <sup>1</sup>              | String  | 5   | Cardholder Zip Code            | Body |
| **Track2** <sup>2</sup>       | String  | 37  | Card Track2 Data (stripe)      | Body |
| **Token** <sup>3</sup>        | String  | 20  | Monetary Token                 | Body |
| **AccountKey** <sup>4</sup>   | String  | 20  | Account Encryption Key         | Body |
| **EncryptedAccount** <sup>4</sup>| String | 224 | Encrypted Account Data Block | Body |
| **Amount**                    | String  | 8   | Transaction Amount             | Body |
| Tip                           | String  | 8   | Tip Amount                     | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier  | Body |
| AuthCode  <sup>5</sup>        | String  | 16  | Voice Authorization Code       | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |
| Trace                         | String  | 40  | Echoed in Response             | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this field for swiped account information.<br />
<sup>3</sup> Include this field for tokenized card information.<br />
<sup>4</sup> Include these fields for encrypted account information.<br />
<sup>5</sup> Include this field for authorizations obtained from the voice authorization center.

<br />

## Capture

`PUT` /credit/preauth/**{RefNo}**

### Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|--------------------------------|----|
| **RefNo**                     | String  | 19  | Transaction RefNo to Capture   | URL  |
| **Token**                     | String  | 20  | Monetary Token                 | Body |
| **Amount** <sup>1</sup>       | String  | 8   | Updated Transaction Amount     | Body |
| **Tip** <sup>1</sup>          | String  | 8   | New or Updated Tip Amount      | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |
| Trace                         | String  | 40  | Echoed in Response             | Body |

<sup>1</sup> Include either or both of these fields.

<br />

## Auth Only

`POST` /credit/authonly

### Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **Account** <sup>1</sup>      | Numeric | 19  | Card Account Number           | Body |
| **Expiration** <sup>1</sup>   | String  | 4   | Card Expiration Date (MMYY)   | Body |
| CVV <sup>1</sup>              | String  | 4   | Card Account CVV              | Body |
| Zip <sup>1</sup>              | String  | 5   | Cardholder Zip Code           | Body |
| **Track2** <sup>2</sup>       | String  | 37  | Card Track2 Data (stripe)     | Body |
| **Token** <sup>3</sup>        | String  | 20  | Monetary Token                | Body |
| **AccountKey** <sup>4</sup>   | String  | 20  | Account Encryption Key         | Body |
| **EncryptedAccount** <sup>4</sup>| String | 224 | Encrypted Account Data Block | Body |
| **Amount** <sup>5</sup>       | String  | 8   | Transaction Amount            | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier | Body |
| AuthCode  <sup>6</sup>        | String  | 16  | Voice Authorization Code      | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |
| Trace                         | String  | 40  | Echoed in Response             | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this field for swiped account information.<br />
<sup>3</sup> Include this field for tokenized card information.<br />
<sup>4</sup> Include these fields for encrypted account information.<br />
<sup>5</sup> `Amount` value may be `0.00` for a zero-dollar (card verification) authorization.<br />
<sup>6</sup> Include this field for authorizations obtained from the voice authorization center.

<br />

## Transaction Detail
Replay transaction response by RefNo.

`GET` /credit/**{RefNo}**

### Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **RefNo**                     | String  | 19  | Transaction RefNo     | URL |

<br />

## Responses

Credit transaction response bodies will include the following fields:

### Response Fields
| Field         | Type    | Max Length  | Description                   |
|---------------|---------|-----|---------------------------------------|
| Status <sup>1</sup>        | String  | 10  | Transaction Status       |
| Message       | String  | 40  | Response Message                      |
| Account       | Numeric | 19  | Masked Card Account Number            |
| Expiration    | String  | 4   | Masked Card Expiration Date           |
| Brand <sup>2</sup>         | String  | 4   | Card Brand               |
| AuthCode      | String  | 16  | Authorization Code                    |
| Amount        | String  | 8   | Transaction Amount                    |
| Tip           | String  | 8   | Tip Amount                            |
| Authorized    | String  | 8   | Amount Authorized                     |
| AVSResult     | String  | 40  | Processor AVS Result                  |
| CVVResult     | String  | 40  | Processor CVV Result                  |
| InvoiceNo     | String  | 10  | Echoed Unique Transaction Identifier  |
| RefNo <sup>3</sup>        | String  | 19  | Transaction Reference Number          |
| Token         | String  | 15 | Account Token                          |
| Trace                         | String  | 40  | Echoed from Request   |

<sup>1</sup> `Status` values: `Approved`, `Declined`, `Success`, or `Error`<br />
<sup>2</sup> `Brand` values: `VISA`, `M/C`, `DCVR`, `AMEX`, `DCLB`, `JCB`, or `OTHER`<br />
<sup>3</sup> Store `RefNo` value for follow-up transaction use.

## Duplicate Checking
Monetary's payment gateway implements standard duplicate checking logic to help avoid multiple accidental charges against a customer's card. Duplicate transactions are detected based on the following request fields matching a transaction which previously approved within the last 24 hours;
* MID (secret key)
* Transaction Type
* Account
* Invoice
* Amount

When a duplicate transaction request is detected, the response returned will be that of the original transaction to which the duplicate transaction matched. Detection of duplicate transactions by the integrator is possible by matching the returned `RefNo` to a to a previous transaction on the client-side.

#### Force Duplicate
In the event that you want to force a duplicate transaction to process, pass the `OverrideDuplicate` request field with the value `true` and duplicate checking will be skipped.
