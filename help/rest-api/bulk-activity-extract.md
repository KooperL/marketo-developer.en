---
title: "Bulk Activity Extract"
feature: REST API
description: "Batch processing Activity data from Marketo."
---

# Bulk Activity Extract

[Bulk Activity Extract Endpoint Reference](https://developer.adobe.com/marketo-apis/api/mapi/)

The Bulk Activity Extract set of REST APIs provides a programmatic interface for retrieving large amounts of activity data out of Marketo.  For cases which do not require low latency, and must transfer significant volumes of activity data out of Marketo, such as CRM-integration, ETL, data warehousing, and data archiving.

## Permissions

The Bulk Activity Extract APIs require that the API user have the "Read-Only Activity" or "Read-Write Activity" permissions.

## Filters

<table>
  <tbody>
    <tr>
      <td>Filter Type</td>
      <td>Data Type</td>
      <td>Required</td>
      <td>Notes</td>
    </tr>
    <tr>
      <td>createdAt</td>
      <td>Date Range</td>
      <td>Yes</td>
      <td>Accepts a JSON object with the members startAt and endAt. startAt accepts a datetime representing the low-watermark, and endAt accepts a datetime representing the high-watermark. The range must be 31 days or fewer.Jobs with this filter type return all accessible records which were created within the date range.Datetimes should be in an ISO-8601 format, without milliseconds.</td>
    </tr>
    <tr>
      <td>activityTypeIds</td>
      <td>Array[Integer]</td>
      <td>No</td>
      <td>Accepts a JSON object with one member, activityTypeIds. The value must be an array of integers, corresponding to the desired activity types.The "Delete Lead" activity is not supported (use <a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getDeletedLeadsUsingGET">Get Deleted Leads</a>endpoint instead).Retrieve activity type ids using the<a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Activities/operation/getActivitiesPagingTokenUsingGET">Get Activity Types</a>endpoint.</td>
    </tr>
    <tr>
      <td>primaryAttributeValueIds</td>
      <td>Array[Integer]</td>
      <td>No</td>
      <td>Accepts a JSON object with one member, primaryAttributeValueIds. The value is an array of ids which specify the primary attributes to filter on. A maximum of 50 ids may be specified.The ids are the unique identifier for either a lead field or an asset, and can be retrieved by calling the appropriate REST API endpoint. For example, to filter on a specific Form for the "Fill Out Form" activity, pass the Form name to <a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET">Get Form by Name</a> endpoint to retrieve the Form Id.The following is a list of activity types where primary attribute filtering is supported.
        <table>
          <tbody>
            <tr>
              <td>Activity Type</td>
              <td>Primary Attribute Value Id</td>
              <td>Retrieval Endpoint</td>
              <td>Asset Group</td>
            </tr>
            <tr>
              <td>Change Data Value</td>
              <td>Lead field id</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2">Describe Lead</a></td>
              <td>Attribute Name</td>
            </tr>
            <tr>
              <td>Change Score</td>
              <td>Lead field id</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2">Describe Lead</a></td>
              <td>Attribute Name</td>
            </tr>
            <tr>
              <td>Change Status in Progression</td>
              <td>Program id</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByNameUsingGET">Get Program by Name</a></td>
              <td>Marketing Program</td>
            </tr>
            <tr>
              <td>Add to List</td>
              <td>Static list id</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET">Get Static List by Name</a></td>
              <td>Static List</td>
            </tr>
            <tr>
              <td>Remove from List</td>
              <td>Static list id</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByNameUsingGET">Get Static List by Name</a></td>
              <td>Static List</td>
            </tr>
            <tr>
              <td>Fill Out Form</td>
              <td>Form id</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Forms/operation/getLpFormByNameUsingGET">Get Form by Name</a></td>
              <td>Web Form</td>
            </tr>
          </tbody>
        </table>
        When using primaryAttributeValueIds, the activityTypeIds filter must be present and only contain activity ids that match the corresponding asset group.Example:For example, if you are filtering on Web Form assets, only the "Fill Out Form" activity type id is allowed in activityTypeIds.Example Request Body:{"filter":{"createdAt":{"startAt": "2021-07-01T23:59:59-00:00","endAt": "2021-07-02T23:59:59-00:00"},"activityTypeIds":[2],"primaryAttributeValueIds" : [16,102,95,8]}}primaryAttributeValueIds and primaryAttributeValues cannot be used together.</td>
    </tr>
    <tr>
      <td>primaryAttributeValues</td>
      <td>Array[String]</td>
      <td>No</td>
      <td>Accepts a JSON object with one member, primaryAttributeValues. The value is an array of names which specify the primary attributes to filter on. A maximum of 50 names may be specified.The names are the unique identifier for either a lead field or an asset, and can be retrieved by calling the appropriate REST API endpoint. For example, to filter on a specific Form for the "Fill Out Form" activity, pass the Form Id to <a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5">Get Form by Id</a> endpoint to retrieve the Form name.The following is a list of activity types where primary attribute filtering is supported.
        <table>
          <tbody>
            <tr>
              <td>Activity Type</td>
              <td>Primary Attribute Value</td>
              <td>Retrieval Endpoint</td>
              <td>Asset Group</td>
            </tr>
            <tr>
              <td>Change Data Value</td>
              <td>Lead field displayName</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2">Describe Lead</a></td>
              <td>Attribute Name</td>
            </tr>
            <tr>
              <td>Change Score</td>
              <td>Lead field displayName</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_2">Describe Lead</a></td>
              <td>Attribute Name</td>
            </tr>
            <tr>
              <td>Change Status in Progression</td>
              <td>Program name</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Programs/operation/getProgramByIdUsingGET">Get Program by Id</a></td>
              <td>Marketing Program</td>
            </tr>
            <tr>
              <td>Add to List</td>
              <td>Static list name</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET">Get Static List by Id</a></td>
              <td>Static List</td>
            </tr>
            <tr>
              <td>Remove from List</td>
              <td>Static list name</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Static-Lists/operation/getStaticListByIdUsingGET">Get Static List by Id</a></td>
              <td>Static List</td>
            </tr>
            <tr>
              <td>Fill Out Form</td>
              <td>Form name</td>
              <td><a href="https://developer.adobe.com/marketo-apis/api/asset/#tag/Sales-Persons/operation/describeUsingGET_5">Get Form by Id</a></td>
              <td>Web Form</td>
            </tr>
          </tbody>
        </table>
        Note that you must use "&lt;<em>program</em>&gt;.&lt;<em>asset</em>&gt;" notation to uniquely specify the name for the following asset groups: Marketing Program, Static List, Web Form.Example:For example, a form with name "MPS Outbound" that resides underneath program with name "GL_OP_ALL_2021" would be specified as "GL_OP_ALL_2021.MPS Outbound".Example Request Body:{"filter":{"createdAt":{"startAt": "2021-07-01T23:59:59-00:00","endAt": "2021-07-02T23:59:59-00:00"},"activityTypeIds":[2],"primaryAttributeValues":["GL_OP_ALL_2021.MPS Outbound"]}}When using primaryAttributeValues, the activityTypeIds filter must be present and only contain activity ids that match the corresponding asset group. For example, if you are filtering on Web Form assets, then only the "Fill Out Form" activity type id is allowed in activityTypeIds.primaryAttributeValues and primaryAttributeValueIds cannot be used together.</td>
    </tr>
  </tbody>
</table>

## Options

| Parameter | Data Type | Required | Notes |
|---|---|---|---|
| filter | Array[Object] | Yes | Accepts an array of filters. Exactly one createdAt filter must be included in the array. An optional activityTypeIds filter may be included.The filters are applied to the accessible activity set, and the resulting set of activities is returned by the export job. |
| format | String | No | Accepts one of: CSV, TSV, SSV The exported file is rendered as a comma-separated values, tab-separated values, or space-separated values file, respectively if set.Defaults to CSV if unset. |
| columnHeaderNames | Object | No | A JSON object containing key-value pairs of field and column header names. The key must be the name of a field included in the export job. The value is the name of the exported column header for that field. |
| fields | Array[String] | No | Optional array of strings containing field values. The listed fields are included in the exported file.By default, the following fields are returned: `marketoGUIDleadId` `activityDate` `activityTypeId` `campaignId` `primaryAttributeValueId` `primaryAttributeValueattributes`,This parameter can be used to reduce the number of fields that are returned by specifying a subset from the list above.Example:"fields": ["leadId", "activityDate", "activityTypeId"]An additional field "actionResult" can be specified to include the activity action ("succeeded", "skipped", or "failed"). |


## Creating a Job

To export records, you first must define the job and the set of records that you want to retrieve.  Create the job using the [Create Export Activity Job](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/createExportActivitiesUsingPOST) endpoint.  When exporting activities there are two primary filters which can be applied: `createdAt`, which is always required, and `activityTypeIds`, which is optional.  The createdAt filter is used to define a date range in which activities were created, using the `startAt` and `endAt` parameters, both of which are datetime fields, and represent the earliest permitted creation date, and the latest permitted creation date respectively.  You may also optionally filter on only certain types of activities, using the `activityTypeIds` filter.  This is useful for removing results which are not relevant for your use case.

```
POST /bulk/v1/activities/export/create.json
```

```json
{ 
   "format": "CSV",
   "filter": { 
      "createdAt": { 
         "startAt": "2017-07-01T23:59:59-00:00",
         "endAt": "2017-07-31T23:59:59-00:00"
      },
      "activityTypeIds": [ 
         1,
         12,
         13
      ]
   }
}
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Created",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "format": "CSV"
      }
   ]
}
```

The job now has a status of "Created," but it is not yet in the processing queue.  To put it in the queue so it can begin processing, we must call the [Enqueue Export Activity Job](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/enqueueExportActivitiesUsingPOST) endpoint using the exportId from the creation status response.

```
POST /bulk/v1/activities/export/{exportId}/enqueue.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Queued",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "format": "CSV"
      }
   ]
}
```

Now the status is reporting that the job has been queued.  When a worker becomes available for this job, then the status is switched to "Processing" and the job will begin aggregating records from Marketo.

## Polling Job Status

Job status can only be retrieved for jobs created by the same API user.

Marketo's Bulk Activity Extract is an asynchronous endpoint, so the job status must be polled to determine when the job is complete.  Poll using the [Get Export Activity Job Status](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/getExportActivitiesStatusUsingGET) endpoint as follows:

```
GET /bulk/v1/activities/export/{exportId}/status.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Completed",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "queuedAt": "2017-01-21T11:48:30-08:00",
         "startedAt": "2017-01-21T11:51:30-08:00",
         "finishedAt": "2017-01-21T12:59:30-08:00",
         "format": "CSV",
         "numberOfRecords": 15423,
         "fileSize": 12342,
         "fileChecksum": "sha256:c16514c7e80fcac5ea055dacae9617fc3c29aff5365e3743071313ce0ed2a815"
      }
   ]
}
```

The status field may respond with one of the following values:

- Created
- Queued
- Processing
- Canceled
- Completed
- Failed

## Retrieving Your Data

Once the job is complete, retrieve your data using the [Get Export Activity File](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/getExportActivitiesFileUsingGET) endpoint.

```
GET /bulk/v1/activities/export/{exportId}/file.json
```

The response contains a file formatted in the way that the job was configured. The endpoint responds with the contents of the file.

If a requested lead field is empty (contains no data), `then null` is placed in the corresponding field in the export file.  In the example below, the campaignId field for the returned activity is empty.

```json
marketoGUID,leadId,activityDate,activityTypeId,campaignId,primaryAttributeValueId,primaryAttributeValue,attributes
783957693,5414087,2022-02-13T14:06:20Z,104,8497,1670,MembershipTest1,"{""Reason"":""Changed by Smart Campaign MembershipTestCampaignStepChoice.MembershipTestCampaignStepChoiceSetUp action Change Data Value"",""Program Member ID"":3240303,""Acquired By"":true,""Old Status"":""Not in Program"",""New Status ID"":21,""Success"":false,""New Status"":""On List"",""Old Status ID"":20}"
783958220,5414094,2022-02-13T14:08:50Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":6,""Success"":true,""New Status"":""Attended"",""Old Status ID"":1}"
783958306,5414094,2022-02-13T14:09:16Z,104,17240,3569,SuccessWebCPS,"{""Program Member ID"":3240305,""Acquired By"":false,""Old Status"":""Attended"",""New Status ID"":6,""Success"":false,""New Status"":""Attended"",""Old Status ID"":6}"
783961924,5316669,2022-02-13T14:27:21Z,104,11614,2333,Nurture Automation,"{""Program Member ID"":3240306,""Acquired By"":false,""Old Status"":""Not in Program"",""New Status ID"":27,""Success"":false,""New Status"":""Member"",""Old Status ID"":26}"
```

To support partial and resumption-friendly retrieval of extracted data, the file endpoint optionally supports the HTTP header `Range` of the type `bytes`.  If the header is not set, the whole of the contents will be returned.  You can read more about using the Range header with Marketo [Bulk Extract](bulk-extract.md).

## Canceling a Job

If a job was configured incorrectly, or becomes unnecessary, it can be easily canceled using the [Cancel Export Activity Job](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Bulk-Export-Activities/operation/cancelExportActivitiesUsingPOST) endpoint:

```
POST /bulk/v1/activities/export/{exportId}/cancel.json
```

```json
{
   "requestId": "e42b#14272d07d78",
   "success": true,
   "result": [
      {
         "exportId": "ce45a7a1-f19d-4ce2-882c-a3c795940a7d",
         "status": "Cancelled",
         "createdAt": "2017-01-21T11:47:30-08:00",
         "format": "CSV"
      }
   ]
}
```

This response has a status indicating that the job has been canceled.
