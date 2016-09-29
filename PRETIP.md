# Monetary Pay API

### Credit PreTip Transaction Requests
* [PreTip](#pretip)
* [PreTip Void](#pretip-void)
* [PreTip Adjust](#pretip-adjust)
* [PreTip Capture](#pretip-capture)

### Credit PreTip Transaction Responses
* [Response Fields](#response-fields)

## PreTip

`POST` /credit/pretip

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| **Account** <sup>1</sup>      | Numeric | 19  | Card Account Number            | Body |
| **Expiration** <sup>1</sup>   | String  | 4   | Card Expiration Date (MMYY)    | Body |
| CVV <sup>1</sup>              | String  | 4   | Card Account CVV               | Body |
| Zip <sup>1</sup>              | String  | 5   | Cardholder Zip Code            | Body |
| **Track2** <sup>2</sup>       | String  | 37  | Card Track2 Data (stripe)      | Body |
| **Token** <sup>3</sup>        | String  | 20  | Monetary Token                 | Body |
| **Amount**                    | String  | 8   | Transaction Amount             | Body |
| Tip                           | String  | 8   | Tip Amount                     | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier  | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this field for swiped account information.<br />
<sup>3</sup> Include this field for tokenized card information.<br />

<br />
## PreTip Void

`POST` /credit/pretip/**{RefNo}**/void

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **RefNo**                     | String  | 19  | Transaction RefNo to Void     | URL |
| **Token**                     | String  | 20  | Monetary Token                | Body |

<br />
## PreTip Adjust

`PUT` /credit/pretip/**{RefNo}**/adjust

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **RefNo**                     | String  | 19  | Transaction RefNo to Void     | URL  |
| **Token**                     | String  | 20  | Monetary Token                | Body |
| **Tip**                       | String  | 8   | Updated Tip Amount            | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction| Body |

<br />
## PreTip Capture

A PreTip transaction that is not captured, will not be settled (i.e. paid to the merchant account).

Only one PreTip Capture should be performed per PreTip since each additional PreTip Caprture performed will result in multiple charges against the cardholder account.

`PUT` /credit/pretip/**{RefNo}**/capture

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|-------------------------------|----|
| **RefNo**                     | String  | 19  | Transaction RefNo to Capture  | URL  |
| **Token**                     | String  | 20  | Monetary Token                | Body |
| **Tip**                       | String  | 8   | Updated Tip Amount            | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction| Body |

<br />
## Responses

Depending upon the merchant's destination processor, the PreTip transactions may not be captured. When a PreTip transaction response includes the `Captured` field as `false`, a `PreTipCapture` transaction must follow in order to successfully capture, in which you can add a `Tip` field. Conversely, when the response includes the `Captured` field as `true`, a `PreTipAdjust` transaction can follow to add a `Tip`, but is not required.

Credit PreTip transaction response bodies will include the following fields:

###Response Fields
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
| InvoiceNo     | String  | 10  | Echoed Unique Transaction Identifier  |
| RefNo <sup>3</sup>        | String  | 19  | Transaction Reference Number          |
| Token         | String  | 15 | Account Token                          |
| Captured <sup>4</sup>      | Boolean |    | Transaction Captured Flag              |

<sup>1</sup> `Status` values: `Approved`, `Declined`, or `Error`<br />
<sup>2</sup> `Brand` values: `VISA`, `M/C`, `DCVR`, `AMEX`, `DCLB`, `JCB`, or `OTHER`<br />
<sup>3</sup> Store `RefNo` value for follow-up transaction use.<br />
<sup>4</sup> `Captured` flag indicates when a followup [PreTip Capture](#pretip-capture) transaction is necessary (when `Captured` = `false`).
