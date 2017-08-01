Title: **Documents Per Site**<br />
Method: **GET**<br />
URL: **[https://www.spvitals.com/powerbi/v1/aggregate/documentsPerSite](https://www.spvitals.com/powerbi/v1/aggregate/documentsPerSite)**<br />

| **Required** | **Parameter** | **Type** | **Description** |
| --- | --- | --- | --- |
| True | customerCode | GUID | This is your unique key. |
| False | fromDate | DATETIME | Records from this date until toDate will be returned. The default is from midnight today. |
| False | filter | STRING | Return records where document names contains filter. |
| False | sites | STRING | Specify which sites to return with. |
| False | skip | INTEGER | Number of records to skip. |
| False | top | INTEGER | Number of records to return. |

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

### Example Request:

```javascript
$.ajax({
  async: true,
  crossDomain: true,
  url: "https://www.spvitals.com/powerbi/v1/aggregate/documentsPerSite?customerCode=00000000-0000-0000-0000-000000000000&fromDate=2017-07-26&filter&sites&skip=&top=",
  method: "GET"
});
```
