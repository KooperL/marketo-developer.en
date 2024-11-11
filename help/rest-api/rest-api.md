---
title: REST API
feature: REST API
description: REST API overview
exl-id: 4b9beaf0-fc04-41d7-b93a-a1ae3147ce67
---
# REST API

Marketo exposes a REST API which allows for remote execution of many of the system's capabilities. From creating programs to bulk lead import, there are many options which allow fine-grained control of a Marketo instance.

These APIs generally fall into two broad categories: [Lead Database](https://developer.adobe.com/marketo-apis/api/mapi/), and [Asset](https://developer.adobe.com/marketo-apis/api/asset/). Lead Database APIs allow for retrieval of, and interaction with Marketo person records and associated object types such as Opportunities and Companies. Asset APIs allow interaction with marketing collateral and workflow-related records.

- **Daily Quota:** Subscriptions are allocated 50,000 API calls per day (which resets daily at 12:00AM CST). You can increase your daily quota through your account manager.
- **Rate Limit:** API access per instance limited to 100 calls per 20 seconds.
- **Concurrency Limit:**  Maximum of ten concurrent API calls.

The size of standard calls is limited to a URI length of 8KB, and a body size of 1MB, though the body can be 10MB for our bulk APIs. If there is an error in with your call, the API will typically still return a status code of 200, but the JSON response will contain a "success" member with a value of `false`, and an array of errors in the "errors" member. More on errors [here](error-codes.md).

## Getting Started

The following steps require admin privileges in your Marketo instance.

For your first call to Marketo, you'll retrieve a lead record. To begin working with Marketo, you must obtain API credentials for making authenticated calls to your instance. Login to your instance and go to the **[!UICONTROL Admin]** -> **[!UICONTROL Users and Roles]**.

![Admin Users and Roles](assets/admin-users-and-roles.png)

Click the **[!UICONTROL Roles]** tab, and then New Role and assign at least the "Read-Only Lead" (or "Read- Only Person") permission to the role in the Access API group. Be sure to give it a descriptive name and click **[!UICONTROL Create]**.

![New Role](assets/new-role.png)

Now back to the [!UICONTROL Users] tab and click **[!UICONTROL Invite New User]**. Give your user a descriptive name that indicates that it is an API user, and an Email Address and click **[!UICONTROL Next]**.

![New User Info](assets/new-user-info.png)

Then, check the [!UICONTROL API Only] option and award your user the API role that you created and click **[!UICONTROL Next]**.

![New User Permissions](assets/new-user-permissions.png)

To complete the user creation process, click **[!UICONTROL Send]**.

![New User Message](assets/new-user-message.png)

Next, go to the [!UICONTROL Admin] menu and click **[!UICONTROL LaunchPoint]**.

![Launchpoint](assets/admin-launchpoint.png)

Click the **[!UICONTROL New]** menu and select **[!UICONTROL New Service]**. Give your service a descriptive name and select **[!UICONTROL Custom]** from the [!UICONTROL Service] dropdown menu. Give it a description, then select your new user from the [!UICONTROL API Only User] dropdown menu and click **[!UICONTROL Create]**.

![New Launchpoint Service](assets/admin-launchpoint-new-service.png)

Click **[!UICONTROL View Details]** for your new service to access the Client ID and Client Secret. For now you can click the **[!UICONTROL Get Token]** button to generate an access token which is valid for one hour. Save the token in a note for now.

![Get Token](assets/get-token.png)

Next, go to the **[!UICONTROL Admin]** menu, then to **[!UICONTROL Web Services]**.

![Web Services](assets/admin-web-services.png)

Find the [!UICONTROL Endpoint] in the REST API box and save in a note for now.

![REST Endpoint](assets/admin-web-services-rest-endpoint-1.png)

When making calls to REST API methods, an access token must be included in every call for the call to be successful. The access token must be sent as a HTTP header.

```
Authorization: Bearer cdf01657-110d-4155-99a7-f986b2ff13a0:int
```

>[!IMPORTANT]
>
>Support for authentication using the **access_token** query parameter is being removed on June 30th 2025. If your project uses a query parameter to pass the access token, it should be updated to use the **Authorization** header as soon as possible. New development should use the **Authorization** header exclusively.

Open a new browser tab and enter the following, using the appropriate information to call [Get Leads by Filter Type](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/getLeadsByFilterUsingGET)

```
<Your Endpoint URL>/rest/v1/leads.json?&filterType=email&filterValues=<Your Email Address>
```

If you don't have a lead record with your email address in your database, substitute it for one that you know is there. Hit enter in your URL bar, and you should get back a JSON response resembling this:

```json
{
    "requestId":"c493#1511ca2b184",
    "result":[
       {
           "id":1,
           "updatedAt":"2015-08-24T20:17:23Z",
           "lastName":"Elkington",
           "email":"developerfeedback@marketo.com",
           "createdAt":"2013-02-19T23:17:04Z",
           "firstName":"Kenneth"
        }
    ],
    "success":true
}

```

## API Usage

Each of your API users is reported individually in the API usage report, so splitting up your web services by user allows you to easily account for the usage of each of your integrations. If the number of API calls to your instance are exceeding the limit and causing subsequent calls to fail, using this practice allows you to account for the volume from each of your services and let you evaluate how to resolve the issue. See your usage by going to **[!UICONTROL Admin]** -> **[!UICONTROL Integration]** > **[!UICONTROL Web Services]** and clicking the number of calls in the past seven days.
