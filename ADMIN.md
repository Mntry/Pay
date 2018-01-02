# Monetary Pay API

### Admin Command Requests
* [Batch Summary](#batch-summary)
* [Batch Close](#batch-close)

### Admin Command Responses
* [Response Fields](#response-fields)

<br />

## Batch Summary

`GET` /admin/batchsummary

### Request Fields

No request fields for Batch Summary Admin Command.

<br />

## Batch Close

`POST` /admin/batchclose

### Request Fields (**bold** fields required)
| Field                         | Type    | Max Length  | Description                   | Location |
|-------------------------------|---------|-----|--------------------------------|------|
| **BatchNo**                   | String  | 6  | Batch number returned in [Batch Summary](#batch-summary)      | Body |
| **BatchItemCount**            | String  | 20  | Batch item count returned in [Batch Summary](#batch-summary) | Body |
| **NetBatchTotal**             | String  | 20  | Net of all transactions in batch returned in [Batch Summary](#batch-summary) | Body |

<br />

## Responses

Admin batch command response bodies will include the following fields:

### Response Fields
| Field         | Type    | Max Length  | Description                   |
|---------------|---------|-----|---------------------------------------|
| Status <sup>1</sup>  | String  | 10  | Transaction Status             |
| Message       | String  | 40  | Optional message from the server or processor |
| BatchNo       | Numeric | 6   | Batch number returned by processor    |
| BatchItemCount| Numeric | 8   | Number of total items in batch        |
| NetBatchTotal | Numeric | 10  | Net of all transactions in batch      |

<sup>1</sup> `Status` values: `Success`, or `Error`<br />
