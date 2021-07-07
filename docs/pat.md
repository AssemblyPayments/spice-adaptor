# Spice Table Server
This is the MX51 Spice Table Server protocol

## Version: 1.0.0

### Terms of service
<https://developer.mx51.io/>

**Contact information:**  
spice@mx51.io  

**License:** [Apache 2.0](https://developer.mx51.io/)

### /ping

#### GET
##### Summary

health check endpoint

##### Description

an endpoint to check the servers health.

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | the server status and support features. |

### /tables

#### GET
##### Summary

Get the list of current tables.

##### Description

This endpoint is used to access the current open tables and their associated bills.

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | A JSON array of open tables. |

### /tables/{table_id}

#### GET
##### Summary

Get an open tables.

##### Description

This endpoint is used to access a specific open table and it's bill.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| table_id | path | The target tables id. | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | details about the given open table. |

### /bills/{bill_id}

#### GET
##### Summary

Get the list of current tables.

##### Description

This endpoint is used to access a specific open table and it's bill.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| bill_id | path | The target tables id. | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | A JSON array of open tables. |

#### POST
##### Summary

Update a table with some payment.

##### Description

This endpoint allows posting a payment against a given bill.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| bill_id | path | The target tables id. | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | A JSON array of open tables. |

### Models

#### Pong

Pong response indicates the servers time and support features.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| pong | string | current time in ISO8601 format. | No |
| features | object | indicate which features this server supports, this is generally used to disable features that server doesn't support. | No |

#### Bill

A bill is the current status of a table

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| billId | string | the current billId, must be globally unique. | Yes |
| tableId | string | the table associated with bill. | Yes |
| totalAmount | number | the total amount for this bill in cents. | Yes |
| outstandingAmount | number | the outstanding amount in cents. | Yes |

#### BillPayment

a purchase event related to current Bill.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| billId | string | the current billId, must be globally unique. | No |
| tableId | string | tableId the table associated with bill. | No |
| operatorId | string | the operator that processed this payment | No |
| paymentType | number | the kind of payment, Cash/Card/et. | No |
| purchaseAmount | number | the amount paid in cents. | No |
| tipAmount | number | something not common in Australia. | No |
| surchargeAmount | number | surcharge amount in cents. | No |
| purchaseResponse | object | The purchase details object, same as Spice Purchase response. | No |

#### OpenTables

An array of OpenTables.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| OpenTables | array | An array of OpenTables. |  |

#### OpenTable

"A table entry indicates information about a given table and it's currently associated bill. tableId is generally a static piece of information, like a physical table number, a booth or bay number while bill.billId is specific for this 'reservation' and should not be reused, similar to a Booking or Reservation ID."

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| tableId | string | the table identifier. | Yes |
| label | string | human friendly table identifier. | No |
| locked | boolean | indicates whatever the current table is locked or not. | No |
| bill |  | A bill is the current status of a table | Yes |
