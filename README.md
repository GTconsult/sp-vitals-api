# SharePoint Vitals API

SharePoint Vitals brings all the user activity data you could ever want to your fingertips.
Now you can access your analytics data through a REST API.

For more information about the client app that captures analytics data, visit [www.sharepointvitals.com](https://www.sharepointvitals.com)

The dashboard for seeing the aggregated data and scheduling reports can be found here: [www.spvitals.com](https://www.spvitals.com)

---

## Version 1.0

This version of the API has had an upgrade to the security layer. Please see the necessary guides to find the changes.

**Executive Summary:**

Instead of sending your customer code (license key) through the URL parameters, this detail must go through the headers. You will also need to include your API key. Navigate to https://www.spvitals.com/PowerBI to generate this API key.

---

## Version 2.0

### Overview

Version 2.0 of the API now has all the reports that you would normally find on the dashboard and more.

Get trend reports or summaries over a selected date range or get a live-stream for a relative period.

### Getting Started

To integrate with SharePoint Vitals API, you will first need to understand how the URL and parameters work. 


The URL made up of components:
**HOST** /api/v2/sharepoint / **TYPE** / **REPORT** ? **PARAMETERS**

### Special Parameters

#### {TYPE}

Name | Description
-|-
summary | The data from this type of report is the same as you would see on the dashboard. It lists each record and it's total number over the period selected.
trend | A trend report shows the number of records as well as the number of total views per day over the selected period.
audit | A combination report of the trend report including the summary report per day.

#### {REPORT}

- activeusers
- pagehits
- visitedsites
- pagehitsperuser
- userspersite
- documentspersite
- documentsperuser
- videoreport
- userhistory
- pageclicks
- searchterms
- devices
- devicesperuser
- browsers
- browsersperuser
- siteaccesshistory
- heatmap

#### {PARAMETERS}

**Please Note:** All the parameters are required, even if their value is empty.

##### Absolute Period - from date to date

Name | Value | Description
-|-|-
fromDate | DATE | The date to select records from. (default is today)
toDate | DATE | The date to select records to. (default is today)
top | NUMBER | Return a limited number of records. For example: top 15 active users. The default is (0) to fetch all records without limit.
skip | NUMBER | Use this to page through large volumes of records.
users | TEXT | Filter the request by a specific user (username in the form user@domain.com). Multiple users can be separated by a comma (,)
sites | TEXT | Filter the request by a specific site. Multiple sites can be separated by a comma (,)
filter | TEXT | Some reports offer filtering specific to the report. For example: Devices, Browsers or Document
orderByCount | BOOLEAN | Sort the records by their count value. Otherwise sort by page load time.
orderDescending | BOOLEAN | Sort records by the largest value first.

#### {PARAMETERS}

##### Relative Period - for some time before today

Name | Value | Description
-|-|-
top | NUMBER | Return a limited number of records. For example: top 15 active users. The default is (0) to fetch all records without limit.
period | TEXT | Name of period to draw reports from. Available options include: **day**, **week**, **month** or **year**
interval | NUMBER | The number of periods to go back, eg. 2 weeks or 3 months

### Error Codes

Status Code | Description
-|-
401 | Unauthorised access if there is a problem verifying your access keys. 
400 | Problem exists with a parameter. 
500 | Exceptions occuring with the API itself.

## Example CURL Request

```curl
curl -X GET \
  'https://www.spvitals.com/api/v2/sharepoint/trend/userspersite?top=25&skip=0&fromDate=2019-01-01&toDate=2019-01-31&users=&sites=&filter=&orderByCount=true&orderDescending=true' \
  -H 'X-SPVITALS-CUSTOMER: 00000000-0000-0000-0000-000000000000' \
  -H 'X-SPVITALS-POWERBI-KEY: 00000000-0000-0000-0000-000000000000' \
```

## Example JavaScript (ajax) Request

```javascript
$.ajax({
  "async": true,
  "crossDomain": true,
  "url": "https://www.spvitals.com/api/v2/sharepoint/trend/userspersite?top=25&skip=0&fromDate=2019-01-01&toDate=2019-01-31&users=&sites=&filter=&orderByCount=true&orderDescending=true",
  "method": "GET",
  "headers": {
    "X-SPVITALS-CUSTOMER": "00000000-0000-0000-0000-000000000000",
    "X-SPVITALS-POWERBI-KEY": "00000000-0000-0000-0000-000000000000"
  }
});
```

## Example Responses

- __Summary Report__ Response 200 (application/json)

        {
            "value": [
                {
                    "user": "maddison.francis@testco.com",
                    "displayName": "Maddison Francis",
                    "count": 205,
                    "averagePageLoadTime": 0
                },
                {
                    "user": "ashton.sutton@testco.com",
                    "displayName": "Ashton Sutton",
                    "count": 189,
                    "averagePageLoadTime": 0
                },
                {
                    "user": "bruno.edwards@testco.com",
                    "displayName": "Bruno Edwards",
                    "count": 149,
                    "averagePageLoadTime": 0
                }
            ]
        }

- __Trend Report__ Response 200 (application/json)

        {
            "value": [
                {
                    "date": "2019-04-01",
                    "recordTally": 31,
                    "totalCount": 733,
                    "summaryData": null
                },
                {
                    "date": "2019-04-02",
                    "recordTally": 29,
                    "totalCount": 679,
                    "summaryData": null
                },
                {
                    "date": "2019-04-03",
                    "recordTally": 0,
                    "totalCount": 0,
                    "summaryData": null
                }
            ]
        }

- __Audit Report__ Response 200 (application/json)

        {
            "value": [
                {
                    "date": "2019-04-01",
                    "recordTally": 3,
                    "totalCount": 733,
                    "summaryData": 
                        {
                            "user": "maddison.francis@testco.com",
                            "displayName": "Maddison Francis",
                            "count": 205,
                            "averagePageLoadTime": 0
                        },
                        {
                            "user": "ashton.sutton@testco.com",
                            "displayName": "Ashton Sutton",
                            "count": 189,
                            "averagePageLoadTime": 0
                        },
                        {
                            "user": "bruno.edwards@testco.com",
                            "displayName": "Bruno Edwards",
                            "count": 339,
                            "averagePageLoadTime": 0
                        }
                    ]
                },
                {
                    "date": "2019-04-02",
                    "recordTally": 3,
                    "totalCount": 679,
                    "summaryData": 
                        {
                            "user": "maddison.francis@testco.com",
                            "displayName": "Maddison Francis",
                            "count": 205,
                            "averagePageLoadTime": 0
                        },
                        {
                            "user": "ashton.sutton@testco.com",
                            "displayName": "Ashton Sutton",
                            "count": 189,
                            "averagePageLoadTime": 0
                        },
                        {
                            "user": "bruno.edwards@testco.com",
                            "displayName": "Bruno Edwards",
                            "count": 285,
                            "averagePageLoadTime": 0
                        }
                    ]
                },
                {
                    "date": "2019-04-03",
                    "recordTally": 3,
                    "totalCount": 543,
                    "summaryData": 
                        {
                            "user": "maddison.francis@testco.com",
                            "displayName": "Maddison Francis",
                            "count": 205,
                            "averagePageLoadTime": 0
                        },
                        {
                            "user": "ashton.sutton@testco.com",
                            "displayName": "Ashton Sutton",
                            "count": 189,
                            "averagePageLoadTime": 0
                        },
                        {
                            "user": "bruno.edwards@testco.com",
                            "displayName": "Bruno Edwards",
                            "count": 149,
                            "averagePageLoadTime": 0
                        }
                    ]
                }
            ]
        }
