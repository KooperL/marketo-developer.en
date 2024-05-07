---
title: Static Lists
feature: REST API, Static Lists
description: "Perform CRUD operations on static lists."
---

# Static lists

[Static Lists Endpoint Reference](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists)

[List Membership Endpoint Reference](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists)

Marketo offers a set of REST APIs for performing CRUD operations on static lists. These APIs follow the standard interface pattern for asset APIs providing Query, Create, Update, and Delete options.

## Query

Querying static lists follows the standard query types for assets of [by id](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET), [by name](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET), and [browse](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListsUsingGET).

### By Id

[Query by id](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET) takes a single static list `id` as a path parameter and returns a single static list record.

```
GET /rest/asset/v1/staticList/{id}.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "843c#1641f969e96",
    "result": [
        {
            "id": 1021,
            "name": "Foundation Seed List",
            "createdAt": "2017-07-27T01:38:33Z+0000",
            "updatedAt": "2017-07-27T01:39:26Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1021A1"
        }
    ]
}
```

#### By Name

[Query by name](https://developer.adobe.com/marketo-apis/api/asset/#tag/Smart-Lists/operation/getSmartListByNameUsingGET) takes a static list `name` as a parameter and returns a single static list record. An exact string match is performed against all static list names in the instance, and returns a result for the static list matching that name.

```
GET /rest/asset/v1/staticList/byName.json?name=Foundation Seed List
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "28ab#1641fa246b9",
    "result": [
        {
            "id": 1021,
            "name": "Foundation Seed List",
            "createdAt": "2017-07-27T01:38:33Z+0000",
            "updatedAt": "2017-07-27T01:39:26Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1021A1"
        }
    ]
}
```

#### Browse

Static lists can also be [retrieved in batches](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListsUsingGET). The `folder` parameter can be used to specify the parent folder under which the query will be performed and is formatted as a JSON object containing id and type. Like other bulk asset retrieval endpoints, `offset` and `maxReturn` are optional parameters that can be used for paging. The `earliestUpdatedAt` and `latestUpdatedAt` parameters allow you to set low and high datetime watermarks for returning static lists created or updated within the given range. Datetime values must be valid ISO-8601 strings, and should not include milliseconds

```
GET /rest/asset/v1/staticLists.json?folder={"id":13,"type":"Folder"}
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "2dc0#1641f846633",
    "result": [
        {
            "id": 1021,
            "name": "Foundation Seed List",
            "createdAt": "2017-07-27T01:38:33Z+0000",
            "updatedAt": "2017-07-27T01:39:26Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1021A1"
        },
        {
            "id": 1022,
            "name": "Blacklist Seed List",
            "createdAt": "2017-07-27T23:19:33Z+0000",
            "updatedAt": "2017-07-27T23:21:29Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1022A1"
        },
        {
            "id": 1023,
            "name": "Possible Duplicates Seed List",
            "createdAt": "2017-07-28T00:10:02Z+0000",
            "updatedAt": "2017-07-28T00:11:22Z+0000",
            "folder": {
                "id": 13,
                "type": "Folder"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1023A1"
        }
    ]
}
```

## Create and Update

[Creating a static list](/asset-/Static_Lists/createStaticListUsingPOST) is executed with an application/x-www-form-urlencoded POST with two required parameters. The `folder` parameter is used to specify the parent folder under which the static list will be created and is formatted as a JSON object containing id and type. The `name` parameter is used to name the static list and must be unique. Optionally the `description` parameter may be used to describe the static list.

```
POST /rest/asset/v1/staticLists.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
folder={"id":1034,"type":"Program"}&name=My Static List
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "1269d#164209d6e1e",
    "result": [
        {
            "id": 1027,
            "name": "My Static List",
            "createdAt": "2018-06-21T04:32:25Z+0000",
            "updatedAt": "2018-06-21T04:32:25Z+0000",
            "folder": {
                "id": 1034,
                "type": "Program"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1027A1"
        }
    ]
}
```

[Updates to a static list](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/updateStaticListUsingPOST) are made through a separate endpoint with two optional parameters. The `description` parameter may be used to update the static list description. The `name` parameter may be used to update the static list name and must be unique.

```
POST /rest/asset/v1/staticList/{id}.json
```

```
Content-Type: application/x-www-form-urlencoded
```

```
description=This is a static list used for testing
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "f84f#16420b4c746",
    "result": [
        {
            "id": 1027,
            "name": "My Static List",
            "description": "This is a static list used for testing",
            "createdAt": "2018-06-21T04:32:26Z+0000",
            "updatedAt": "2018-06-21T04:57:55Z+0000",
            "folder": {
                "id": 1034,
                "type": "Program"
            },
            "computedUrl": "https://app-sjqe.marketo.com/#ST1027A1"
        }
    ]
}
```

### Delete

[Deleting a static list](https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/deleteStaticListByIdUsingPOST) takes a single static list `id` as a path parameter. Deletions cannot be made to static lists that are in use by an import or export operation, or are in use by other assets.

```
POST /rest/asset/v1/staticList/{id}/delete.json
```

```json
{
    "success": true,
    "errors": [],
    "requestId": "2c79#16420ded0e9",
    "result": [
        {
            "id": 1027
        }
    ]
}
```

## List Membership

The list membership endpoints provide ability to add, remove, and query static list members. In addition, you can query static list membership.

### Add to List

The [Add to List](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/addLeadsToListUsingPOST) endpoint is used add one or more members to a list. The endpoint takes a required `listId` path parameter, and one or more id query parameters which contain lead ids (maximum allowed is 300).

The response contains a `result` array comprised of JSON objects with the status for each lead id that was specified in the request.

```
POST /rest/v1/lists/{listId}/leads.json?id=318594&id=318595
```

```json
{
    "requestId": "6860#1706170ba29",
    "result": [
        {
            "id": 318594,
            "status": "added"
        },
        {
            "id": 318595,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1004",
                    "message": "Lead not found"
                }
            ]
        }
    ],
    "success": true
}
```

### Remove from List

The [Remove from List](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/removeLeadsFromListUsingDELETE) endpoint is used remove one or more members from a list. The endpoint takes a required `listId` path parameter, and one or more `id` query parameters which contain lead ids (maximum allowed is 300).

The response contains a `result` array comprised of JSON objects with the status for each lead id that was specified in the request.

```
DELETE /rest/v1/lists/{listId}/leads.json?id=318603&id=318595&id=999999
```

```
{
    "requestId": "9e79#17061689ac3",
    "result": [
        {
            "id": 318603,
            "status": "removed"
        },
        {
            "id": 318595,
            "status": "removed"
        },
        {
            "id": 999999,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1004",
                    "message": "Lead not found"
                }
            ]
        }
    ],
    "success": true
}
```

### Query List

The [Get Leads by List Id](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/getLeadsByListIdUsingGET) endpoint is used to retrieve members of a list. The endpoint takes a required `listId` path parameter, and allows several optional query parameters to specify filtering criteria.

The `batchSize` parameter is used to specify the number of lead records to be returned in a single call (default and max is 300).

The `nextPageToken` parameter is used to paginate through large result sets. This parameter is not passed in the first call, but only in subsequent calls for the pagination.

The `fields` parameter contains a comma-separated list of field names to be returned in the response. If the fields parameter is not included in this request, the following default fields are returned: email, updatedAt, createdAt, lastName, firstName, and id.

The response contains a `result` array comprised of JSON objects containing the lead fields that were specified in the request.

```
GET /rest/v1/lists/{listId}/leads.json?batchSize=3
```

```json
{
    "requestId": "ddae#170615ba0cc",
    "result": [
        {
            "id": 318594,
            "firstName": "Hanna",
            "lastName": "Crawford",
            "email": "208161Robert.L.Deacon@pookmail.com",
            "updatedAt": "2015-04-06T17:13:50Z",
            "createdAt": "2015-04-06T17:13:50Z"
        },
        {
            "id": 318595,
            "firstName": "Bertha",
            "lastName": "Fulton",
            "email": "208160Tyrone.V.Dyer@trashymail.com",
            "updatedAt": "2015-04-06T17:13:50Z",
            "createdAt": "2015-04-06T17:13:50Z"
        },
        {
            "id": 318596,
            "firstName": "Faith",
            "lastName": "England",
            "email": "208159Rex.M.Bailey@dodgit.com",
            "updatedAt": "2015-04-06T17:13:50Z",
            "createdAt": "2015-04-06T17:13:50Z"
        }
    ],
    "success": true,
    "nextPageToken": "PS5VL5WD4UOWGOUCJR6VY7JQO24LC2U5DRBU4WO4RQMPHDHTK2T3BEZOR75VLQXYB3245WW2GMDSK==="
}
```

#### Query List Membership by Lead Id

The [Member of List](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Static-Lists/operation/areLeadsMemberOfListUsingGET) endpoint is used to see if one or more leads are members of a list. The endpoint takes a required `listId` path parameter, and one or more `id` query parameters which contain lead ids (maximum allowed is 300).

The response contains a `result` array comprised of JSON objects with the status for each lead id that was specified in the request.

```
GET /rest/v1/lists/{listId}/leads/ismember.json?id=309901&id=318603&id=999999
```

```json
{
    "requestId": "693a#17061475cf9",
    "result": [
        {
            "id": 309901,
            "status": "memberof"
        },
        {
            "id": 318603,
            "status": "notmemberof"
        },
        {
            "id": 999999,
            "status": "skipped",
            "reasons": [
                {
                    "code": "1004",
                    "message": "Lead not found"
                }
            ]
        }
    ],
    "success": true
}
```
