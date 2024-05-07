---
title: "SOAP API"
feature: Reporting
description: "Marketo SOAP overview"
---

# SOAP API

The SOAP API is no longer under active development. The calls still function, but our development is focused on [REST](/rest-api/) going forward.

The Marketo SOAP API allows for the creation, retrieval, and removal of [entities and data](/getting-started/) stored within Marketo. You can find the [Marketo-SOAP-SDK](https://github.com/Marketo/SOAP-API-Java-Client) on GitHub. There are also [client libraries](https://github.com/Marketo/Community-Supported-Client-Libraries) to save you some time.

Latest API Version: 3_1

## SOAP WSDL

To retrieve the SOAP WSDL document, obtain your SOAP API Endpoint from your **Admin** > **Integration** > **Web Services** menu. 

![SOAP Endpoint](assets/endpoint-soap.png)

Your WSDL URL is:

`<SOAP API Endpoint> + ?WSDL`

Do not use the end point defined in the WSDL. Each Marketo instance has a unique end point in which to make calls to.

## Limits

- **Daily Quota:** Most subscriptions are allocated 10,000 API calls per day (which resets daily at 12:00AM CST). You can increase your daily quota through your account manager.
- **Rate Limit:** API access per instance limited to 100 calls per 20 seconds.
- **Concurrency Limit:**  Maximum of ten concurrent API calls.

Our recommendation is that batch sizes are no larger than 300. Larger sizes are not supported and may result in timeouts, and in extreme cases being throttled.

## SOAP API settings in Marketo

1. Go to the Admin section and click Web Services.

![admin-web-services2](assets/admin-web-services2.png)

1. Set an appropriate Encryption Key, click "Save Changes" and use the SOAP API Endpoint, User ID, and Encryption Key values to generate the correct [authentication signature](/soap-api/authentication-signature/) for each SOAP API call.

![admin-web-services3](assets/admin-web-services3.png)
