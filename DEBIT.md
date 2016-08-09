# Monetary Pay API

### Debit Transaction Requests
* [Sale](#sale)
* [Return](#return)

### Debit Transaction Responses
* [Response Fields](#response-fields)

## Sale

`POST` /debit/sale

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| **Track2**                    | String  | 37  | Card Track2 Data (stripe)      | Body |
| **DerivedKey**                | String  | 20  | Debit Derived Key              | Body |
| **PINBlock**                  | String  | 20  | Debit PIN Block                | Body |
| **Amount**                    | String  | 8   | Transaction Amount             | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier  | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |

<br />
## Return

`POST` /debit/return

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| **Track2**                    | String  | 37  | Card Track2 Data (stripe)      | Body |
| **DerivedKey**                | String  | 20  | Debit Derived Key              | Body |
| **PINBlock**                  | String  | 20  | Debit PIN Block                | Body |
| **Amount**                    | String  | 8   | Transaction Amount             | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier  | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |


<br />
## Responses

Debit transaction response bodies will include the following fields:

###Response Fields
| Field         | Type    | Max Length  | Description                   |
|---------------|---------|-----|---------------------------------------|
| Status <sup>1</sup>        | String  | 10  | Transaction Status                    |
| Account       | Numeric | 19  | Masked Card Account Number            |
| Expiration    | String  | 4   | Masked Card Expiration Date           |
| Brand <sup>2</sup>         | String  | 4   | Card Brand                            |
| Amount      | String  | 8   | Transaction Amount                       |
| Authorized    | String  | 8   | Amount Authorized                     |
| InvoiceNo     | String  | 10  | Echoed Unique Transaction Identifier  |
| RefNo <sup>3</sup>        | String  | 10  | Transaction Reference Number          |

<sup>1</sup> `Status` values: `Approved`, `Declined`, `Success`, or `Error`<br />
<sup>2</sup> `Brand` values: `Debit`<br />
<sup>3</sup> Store `RefNo` value for follow-up transaction use.
