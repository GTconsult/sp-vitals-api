# SharePoint Vitals API

SharePoint Vitals brings all the user activity data you could ever want to your fingertips.
Now you can access your analytics data through a REST API.

For more information about the client app that captures analytics data, visit [www.sharepointvitals.com](https://www.sharepointvitals.com)

The dashboard for seeing the aggregated data and scheduling reports can be found here: [www.spvitals.com](https://www.spvitals.com)

<hr />

## Version 1.0

This version of the API has had an upgrade to the security layer. Please see the necessary guides to find the changes.

**Executive Summary:** 

Instead of sending your customer code (license key) through the URL parameters, this detail must go through the headers. You will also need to include your API key. Navigate to https://www.spvitals.com/PowerBI to generate this API key.

<hr />

## Version 2.0

### Overview
Get trend reports or summaries over a selected date range or get a live-stream for a relative period.

### Error Codes
Status Code | Description
-|-
401 | Unauthorised access if there is a problem verifying your access keys. 
400 | Problem exists with a parameter. 
500 | Exceptions occuring with the API itself.

### Special Parameters
#### {type} 
Name | Description
-|-
summary | Total number of views per resource for the selected period.
trend | A report showing the number of records as well as the number of total views per day over the selected period.
audit | A combination report of the trend report including the summary report per day.

#### {report}
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


### Authentication
Generate an API key through the SharePoint Vitals dashboard and include it with your existing license key in the request header.
Navigate to https://www.spvitals.com/PowerBI to generate an API key.

Key | Value
-|-
X-SPVITALS-CUSTOMER | xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
X-SPVITALS-POWERBI-KEY | xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## Absolute Period
Enter a custom date range between 2 points in time.

### api/v2/sharepoint/{type}/{report}?parameters [GET]

- Request Parameters

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

## Example Responses

+ __Summary__ Report Response 200 (application/json)

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

+ __Trend__ Report Response 200 (application/json)

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

+ __Audit__ Report Response 200 (application/json)

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
