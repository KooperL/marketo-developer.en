---
title: Download Swagger Definitions
feature: REST API, Programs
description: Download Swagger definition files for local consumption.
exl-id: c2bed094-36f9-47e7-a6d5-c237e425966a
---
# Download Swagger Definitions

[Swagger](https://swagger.io/) or [OpenAPI](https://www.openapis.org/) definitions are data files that describe all the methods and parameters of a REST API. You can download and consume these data files locally as your personal API reference.

To use the Marketo Engage Swagger/OpenAPI definitions, the `host` field of each document must be updated to match the REST API hostname from your Marketo Engage instance.

First, download the OpenAPI definition you want to use: 

* [Asset](assets/swagger-asset.json)
* [Lead](assets/swagger-mapi.json)
* [Identity](assets/swagger-identity.json)
* [User Management](assets/swagger-user.json)

Next, obtain your REST API hostname from the Marketo Admin. Go to the _Admin_-> _Web Services_ menu in Marketo Engage and copy the hostname from the Endpoint field. The `hostname` is the string between the protocol, `https://`, and `/rest`, which looks like `AAA-999-AAA.mktorest.com` 

Open your OpenAPI file in a text editor and find the `host` field in the JSON and change its value to your REST API hostname: `"host":"localhost:8080"` to `"host":"AAA-999-AAA.mktorest.com"`.

Once saved, you can run the definition file in your Swagger UI instance or any other OpenAPI software.
