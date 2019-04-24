# Documents Per Site<br />
Version: **1.0**<br />
Method: **GET**<br />
URL: **[https://www.spvitals.com/powerbi/v1/aggregate/documentsPerSite](https://www.spvitals.com/powerbi/v1/aggregate/documentsPerSite)**<br />

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
| False | fromDate | DATETIME | Records from this date until toDate will be returned. The default is from midnight today. |
| False | filter | STRING | Return records where document names contains filter. |
| False | sites | STRING | Specify which sites to return with. |
| False | top | INTEGER | Number of records to return. |
| False | skip | INTEGER | Number of records to skip. |

### Success Response: 200 OK

```json
[
  {
      "documentName": "",
      "documentLibrary": "",
      "documentUrl": "",
      "siteName": "",
      "count": 0
  }
]
```

### Error Responses:

| **Status** | **Reason** |
| --- | --- |
| 400 Bad Request | One of the required parameters data type is incorrect. |
| 401 Unauthorized | Customer code does not exist or has been revoked. |
| 404 Not Found | A parameter is missing or mistyped. |
| 500 Internal Server Error | An unexpected server error. |

### Example CURL Request:

```curl
curl -X GET \
  'https://www.spvitals.com/powerbi/v1/aggregate/documentsPerSite?fromDate=2019-04-24&filter=&sites=&skip=0&top=10' \
  -H 'X-SPVITALS-CUSTOMER: 00000000-0000-0000-0000-000000000000' \
  -H 'X-SPVITALS-POWERBI-KEY: 00000000-0000-0000-0000-000000000000'
```

### Example Request:

```javascript
$.ajax({
  "url": "https://www.spvitals.com/powerbi/v1/aggregate/documentsPerSite?fromDate=2019-04-24&filter=&sites=&skip=0&top=10",
  "method": "GET",
  "headers": {
    "X-SPVITALS-CUSTOMER": "00000000-0000-0000-0000-000000000000",
    "X-SPVITALS-POWERBI-KEY": "00000000-0000-0000-0000-000000000000"
  }
});
```
