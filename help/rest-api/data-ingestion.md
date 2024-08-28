---
title: Data Ingestion
feature: REST API, Dynamic Content
description: Consume data with Marketo APIs.
exl-id: 1d501916-53ac-42d8-a804-abb4ab01c7e8
---
# Data Ingestion API

The Data Ingestion API is a high volume, low latency, highly available service designed to handle ingestion of large amounts of person and person related data efficiently and with minimal delays. 

Data is ingested by submitting requests that execute asynchronously. Request status can be retrieved by subscribing to events from the [Marketo Observability Data Stream](https://developer.adobe.com/events/docs/guides/using/marketo/marketo-observability-data-stream-setup/).​

Interfaces are offered for two object types: Persons, Custom Objects. The record operation is "insert or update" only.

The Data Ingestion API is currently in private beta.  Invitees are required to have an entitlement for [Marketo Engage Performance Tier](https://nation.marketo.com/t5/product-documents/marketo-engage-performance-tiers/ta-p/328835) Package.

## Authentication

The Data Ingestion API uses the same OAuth 2.0 authentication method as Marketo REST API to generate an access token, but the access token must be passed via HTTP header `X-Mkto-User-Token`. You cannot pass the access token via a query parameter.

Example Access Token via Header:

`X-Mkto-User-Token: 11606815-aa7a-405a-80a1-f9683efa528b:ab`

## Permissions

Data Ingestion uses the same permissions model as the Marketo REST API, and does not require any additional special permissions to use, though specific permissions are required for each endpoint.

|Endpoint  | Permission|
|-|-|
|Persons  | Read-Write Lead|
|Custom Objects  | Read-Write Custom Object|

## Headers

Data Ingestion makes use of the following custom HTTP headers.

### Request

| Key  |   Value  |   Required   |  Description |
| - | - | - | - |
|X-Correlation-Id   |  Arbitrary string (maximum length 255 characters).  |   No  |   Can be used to trace requests through the system.  See Marketo Observability Data Stream|
|X-Request-Source   |  Arbitrary string (maximum length 50 characters).   |  No  |   Can be used to trace the source of requests through the system.  See Marketo Observability Data Stream|

### Response

| Key   |  Value   |  Required  |
| - | - | - |
| X-Request-Id   |   Unique request ID.  |  Yes   |

## Requests

Use the HTTP POST method to send data to the server.

The data representation is included in the request body as application/json.

The domain name is: `mkto-ingestion-api.adobe.io`

The path begins with `/subscriptions/MunchkinId` where MunchkinId is specific to your Marketo instance. You can find your Munchkin ID in the Marketo Engage UI under **Admin** > **My Account** > **Support Information**.  The remainder of the path is used to specify the resource of interest.

Example URL for Persons:

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/persons`

Example URL for Custom Objects:

`https://mkto-ingestion-api.adobe.io/subscriptions/556-RJS-213/customobjects/purchases`

### Responses

All responses return a unique request ID via the `X-Request-Id` header.

Example of request ID via header:

`X-Request-Id: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### Success

When a call is successful, a 202 status is returned.  No response body is returned.

Example of Success Response:

```
HTTP/1.1 202 Accepted
X-Request-Id: e3d92152-0fb1-444a-8f8f-29d5a2338598
Content-Length: 0
Date: Wed, 18 Oct 2023 18:56:49 GMT
```

### Error

When a call produces an error, a non-202 status is returned along with a response body with additional error detail.  The response body is application/json and contains a single object with members error_code and message.

Below are reused error codes from Adobe Developer Gateway.

| HTTP Status Code  |   error_code   |  message|
| - | - | - |
|401  |   401013  |  Oauth token is invalid|
|403  |   403010  |   Oauth token is missing|
|404  |   404040  |  Resource not found|
|429  |   429001  |   Service usage limit reached|

Below are error codes that are unique to the Data Ingestion API and are comprised of 3 segments.  The first three digits are the status (returned by Adobe Developer Gateway), followed by a zero "0", followed by three digits.

| HTTP Status Code  |   error_code  |   message|
| - | - | - |
|400  |   4000801  |   Bad request|
|400  |   4000802  |   Invalid data|
|403  |   4030801  |   Unauthorized|
|429  |   4290801  |   Daily quota reached|
|500  |   5000801   |  Internal Server Error|

## Retries

When a transient error is detected, the service retries the operation three times.  The first retry occurs after a 5  minute wait period, the second after 30 more minutes, and finally the third after 30 more minutes.  Retries happen for various reasons, primarily when a dependent service times out or is temporarily not available.

## Endpoints

Ingestion endpoints are available for Persons and Custom Objects.

### Persons

Endpoint used to upsert person records.

| Method | Path |
| - | - |
| POST | /subscriptions/{munchkinId}/persons |

#### Headers

| Key  |   Value |
| - | - |
| Content-Type  |   application/json |
| X-Mkto-User-Token  |   {accessToken} |

#### Request body

| Key   |  Data Type  |   Required  |   Value  |   Default Value|
| - | - | - | - | - |
| priority  |   String  |   No  |   Priority of the request: normal or high  |  normal |
|partitionName   |  String   |  No   |  Name of person partition  |   Default|
|dedupeFields  |   Object   |  No  |   Attributes to deduplicate on. One or two attribute names are allowed. <br/> Two attributes are used in an AND operation. For example, if both `email` and `firstName` are specified, they are both used to look up a person using the AND operation. <br/>Supported attributes are: `id`, `email`, `sfdcAccountId`, `sfdcContactId`, `sfdcLeadId` `sfdcLeadOwnerId`, Custom attributes ("string" and "integer" type only),  `email` |
|persons   |  Array of Object  |   Yes   |  List of attribute name-value pairs for the person   |  – |

Permissions required are `Read-Write Lead`.

### Persons example

#### Request

`POST /subscriptions/{munchkinId}/persons`

#### Headers

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### Body

```json
{
   "priority": "high",
   "partitionName": "EMEA",
   "dedupeFields": {
      "field1": "email",
      "field2": "firstName"
   },
   "persons":[
      {
         "email": "brooklyn.parker@karnv.com",
         "firstName": "Brooklyn",
         "lastName": "Parker"
      },
      {
         "email": "johnny.neal@yvu30.com",
         "firstName": "Johnny",
         "lastName": "Neal"
      }
   ]
}
```

#### Response

`HTTP/1.1 202`
`X-Request-ID: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

### Custom Objects

Endpoint used to upsert custom object records

| Method | Path |
| - | - |
| POST | `/subscriptions/{munchkinId}/customobjects/{customObjectAPIName}` |

#### Headers

| Key  |   Value |
| - | - |
| Content-Type  |   application/json |
| X-Mkto-User-Token  |   {accessToken} |

#### Request body

| Key  |    Data Type |    Required  |    Value    |  Default Value |
| - |- | - | - | - |
| priority  |  String  | No  |  Priority of the request: normal, high |   normal |
| dedupeBy  |  String  | No  |  Attributes to deduplicate on: dedupeFields, marketoGUID |   dedupeFields |
| customObjects |  Array of Object | Yes | List of attribute name-value pairs for the object. | – |

Required permissions are `Read-Write Custom Object`.

If a link field to a Person is specified in the request and that Person does not exist, several retries occur. If that Person is added during the retry window (65 minutes), then the update is successful. For example, if the link field is email on Person, and Person does not exist, then a retries occur.

### Custom Objects example

#### Request

`POST /subscriptions/{munchkinId}/customobjects/{customObjectAPIName}`
    

#### Headers

`Content-Type: application/json`
`X-Mkto-User-Token: {accessToken}`

#### Body

```json
{
   "dedupeBy": "dedupeFields",
   "priority": "high",
   "customObjects": [
      {
         "email": "brooklyn.parker@karnv.com",
         "vin": "20UYA31581L000000",
         "make": "BMW",
         "model": "3-Series 330i",
         "year": 2003
      },
      {
         "email": "johnny.neal@yvu30.com",
         "vin": "19UYA31581L000000",
         "make": "BMW",
         "model": "3-Series 325i",
         "year": 1989
      }
   ]
}
```

#### Response

`HTTP/1.1 202`
`X-Request-ID: WOUBf3fHJNU6sTmJqLL281lOmAEpMZFw`

## Limits

Here is a list of usage of guardrails:

* Maximum size of request: 1 MB
* Maximum objects per request per object type: 1,000
* Maximum requests per second per client ID: 5,000
* Maximum objects per day: 10,000,000

## Data Ingestion API vs REST API

Here is a list of differences between Data Ingestion API and other Marketo REST APIs:

* This is not a full CRUD interface, it supports upsert only
* To authenticate, you must pass access token using the `X-Mkto-User-Token` header
* The URL domain name is `mkto-ingestion-api.adobe.io`
* The URL path begins with `/subscriptions/MunchkinId`
* There are no query parameters
* If the call is successful, a 202 status is returned and the response body is empty
* If call fails, a non-202 status is returned and the response body contains `{ "error_code" : "Error Code", "message" : "Message" }`
* The request ID is returned via `X-Request-Id` header
