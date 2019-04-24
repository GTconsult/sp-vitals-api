# Active Users<br />
Version: **1.0**<br />
Method: **GET**<br />
Endpoint URL: **[https://www.spvitals.com/powerbi/v1/aggregate/user](https://www.spvitals.com/powerbi/v1/aggregate/user)**<br />

## API Key

Your API key can be obtained by going to [https://www.spvitals.com/PowerBi](https://www.spvitals.com/PowerBi) and generating a key.

## Headers

Key | Value | Description
-|-|-
X-SPVITALS-CUSTOMER | GUID | This is your unique licence key.
X-SPVITALS-POWERBI-KEY | GUID | PowerBI API key.

## Parameters

| **Required** | **Parameter** | **Type** | **Description** |
| --- | --- | --- | --- |
| False | fromDate | DATETIME | Records from this date until today will be returned. The default is from midnight today until now. |
| False | top | INTEGER | Number of records to return. |
| False | skip | INTEGER | Number of records to skip. |
| False | orderByCount | BOOLEAN | If this is true, then records will be sorted by number of hits. |
| False | orderDescending | BOOLEAN | If this is true, then records will be sorted by the largest value first. |

### Success Response: 200 OK

```json
[
    {
        "user": "",
        "displayName": "",
        "count": 0,
        "averagePageLoadTime": 0.0
    },
    {
        "user": "",
        "displayName": "",
        "count": 0,
        "averagePageLoadTime": 0.0
    }
]
```

### Error Responses:

| **Status** | **Reason** |
| --- | --- |
| 400 Bad Request | One of the parameters data type is incorrect. |
| 401 Unauthorized | Customer code does not exist or has been revoked. |
| 404 Not Found | A parameter is missing or mistyped. |
| 500 Internal Server Error | An unexpected server error. |

### Example Request:

```javascript
$.ajax({
  async: true,
  crossDomain: true,
  url: "https://www.spvitals.com/powerbi/v1/aggregate/user?customerCode=00000000-0000-0000-0000-000000000000&top=&skip=&orderByCount=true&orderDescending=true&fromDate=2017-07-28",
  method: "GET"
});
```
