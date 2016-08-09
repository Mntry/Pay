# Monetary Pay API

### Stored Value Transaction Requests
* [Load](#load)
* [Void Load](#void-load)
* [Sale](#sale)
* [Void Sale](#void-sale)
* [Balance](#balance)
* [Create](#create)
* [Set](#set)

### Stored Value Transaction Responses
* [Response Fields](#response-fields)

## Load

`POST` /storedvalue/load

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description            | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| **Account** <sup>1</sup>      | Numeric | 19  | Account Number                 | Body |
| CVV <sup>1</sup>              | String  | 3   | Account CVV                    | Body |
| **Track2** <sup>2</sup>       | String  | 50  | Track2 Data (stripe)           | Body |
| **Identifier** <sup>3</sup>   | String  | 30  | Account Alternate Identifier   | Body |
| **Amount**                    | Numeric | 8   | Transaction Amount             | Body |
| OverrideCVV                   | Boolean |     | Override Account CVV           | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier  | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |
| AdjustPoints                  | Numeric | 11  | Adjust Points Balance Amount   | Body |
| Promo                         | Boolean |     | Promotional Load               | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this field for swiped account information.<br />
<sup>3</sup> Include this field alternate identifier account information.

<br />

## Void Load

`POST` /storedvalue/load/**{RefNo}**/void

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description            | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| **RefNo**                     | String  | 19  | Transaction RefNo to Void      | URL |

<br />

## Sale

`POST` /storedvalue/sale

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description            | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| **Account** <sup>1</sup>      | Numeric | 19  | Account Number            | Body |
| CVV <sup>1</sup>              | String  | 3   | Account CVV               | Body |
| **Track2** <sup>2</sup>       | String  | 50  | Track2 Data (stripe)      | Body |
| **Identifier** <sup>3</sup>   | String  | 30  | Account Alternate Identifier   | Body |
| **Amount**                    | Numeric | 8   | Transaction Amount             | Body |
| OverrideCVV                   | Boolean |     | Override Account CVV           | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier  | Body |
| OverrideDuplicate             | Boolean |     | Override Duplicate Transaction | Body |
| AdjustPoints                  | Numeric | 11  | Adjust Points Balance Amount   | Body |
| NoNSF                         | Boolean |     | No Non-Sufficient Funds        | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this field for swiped account information.<br />
<sup>3</sup> Include this field alternate identifier account information.

<br />

## Void Sale

`POST` /storedvalue/sale/**{RefNo}**/void

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description            | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| **RefNo**                     | String  | 19  | Transaction RefNo to Void      | URL |

<br />

## Balance

`POST` /storedvalue/balance

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description            | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| **Account** <sup>1</sup>      | Numeric | 19  | Account Number            | Body |
| CVV <sup>1</sup>              | String  | 3   | Account CVV               | Body |
| **Track2** <sup>2</sup>       | String  | 50  | Track2 Data (stripe)      | Body |
| **Identifier** <sup>3</sup>   | String  | 30  | Account Alternate Identifier   | Body |
| OverrideCVV                   | Boolean |     | Override Account CVV           | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this field for swiped account information.<br />
<sup>3</sup> Include this field alternate identifier account information.

<br />

## Create

`POST` /storedvalue/create

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description            | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| Amount                        | Numeric | 8   | Transaction Amount             | Body |
| **Identifier**                | String  | 30  | Account Alternate Identifier   | Body |
| NewIdentifier                 | String  | 30  | New Account Alternate Identifier | Body |
| InvoiceNo                     | String  | 10  | Unique Transaction Identifier  | Body |
| AdjustPoints                  | Numeric | 11  | Adjust Points Balance Amount   | Body |
| Promo                         | Boolean |     | Promotional Load               | Body |
| Lock                          | Boolean |     | Account Lock                   | Body |

<br />

## Set

`POST` /storedvalue/set

###Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description              | Location |
|-------------------------------|---------|-----|----------------------------------|------|
| **Account** <sup>1</sup>      | Numeric | 19  | Account Number              | Body |
| CVV <sup>1</sup>              | String  | 3   | Account CVV                 | Body |
| **Track2** <sup>2</sup>       | String  | 50  | Track2 Data (stripe)        | Body |
| **Identifier** <sup>3</sup>   | String  | 30  | Account Alternate Identifier     | Body |
| OverrideCVV                   | Boolean |     | Override Account CVV             | Body |
| NewIdentifier                 | String  | 30  | New Account Alternate Identifier | Body |
| Lock                          | Boolean |     | Account Lock                     | Body |

<sup>1</sup> Include these fields for manually entered account information.<br />
<sup>2</sup> Include this field for swiped account information.<br />
<sup>3</sup> Include this field alternate identifier account information.

<br />

## Responses

Stored Value transaction response bodies include the following fields:

###Response Fields
| Field         | Type    | Max Length  | Description                   |
|---------------|---------|-----|---------------------------------------|
| Status <sup>1</sup> | String  | 50  | Transaction Status              |
| Message       | String  | 50 | Response Message                       |
| Account       | Numeric | 19 | Account Number                         |
| CVV           | String  | 3  | Account CVV                            |
| Identifier    | String  | 30 | Account Alternate Identifier           |
| Amount        | Numeric | 8  | Transaction Amount                     |
| Balance       | Numeric | 8  | Account Balance                        |
| AdjustPoints  | Numeric | 11 | Adjust Points Amount                   |
| Points        | Numeric | 11 | Points Balance                         |
| RefNo         | String  | 19 | Transaction RefNo                      |
| InvoiceNo     | String  | 16 | Unique Transaction Identifier          |
| AdjustPoints  | Numeric | 11 | Adjust Points Balance Amount           |
| Promo         | Boolean |    | Promotional Load                       |
| Lock          | Boolean |    | Account Locked                         |
| Voided        | Boolean |    | Transaction Voided                     |
| Code          | String  | 10 | Account Code                           |

<sup>1</sup> `Status` values: `Approved`, `Duplicate`, `Declined`, or `Error`<br />
