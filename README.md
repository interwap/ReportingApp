## Documentation
The ReportingApp API is the primary way for apps to read and write to the ReportingApp Backend Service. We cover the basics of ReportingApp API terminology and structure in the ReportingApp API overview. This document goes into more detail about the various operations you can perform with the ReportingApp API.

## HTTP/1.1
All data transfers conform to HTTP/1.1, and all endpoints require HTTP/HTTPS. We have also enabled the includeSubdomains HSTS directive on charleyapp.com, but this should not adversely affect your ReportingAPP API calls.

## Host URL
Almost all requests are passed to the **reporting.charleyapp.com/api** host URL. All request content-type are application/x-www-form-urlencoded and response are json.

## Access Tokens
Access tokens allow your app to access the ReportingApp API. They typically perform two functions:

1. they allow your app to access a User's information without requiring the User's password, and
2. they allow us to identify your app, the User who is using your app, and the type of data the User has permitted your app to access.
All ReportingApp API endpoints require an access token of some kind, so each time you access an endpoint, your request must include one.
The app and User IDs are both encoded in the token itself (among other things), and we use those IDs to keep track of which data the User has permitted the app to access.

## Login

------------ | -------------
Description | Authenticating user handles user accounts, groups, permissions and cookie-based user sessions
URL | /authenticate
Method | GET
Parameters | id & password

###### Response
```
{
    "success": true,
    "title": "Request Successful.",
    "access_token": "lgwx8nwrvKD",
    "username": "johndoe",
    "staff_id": "JD23S4",
    "email": "johndoe@charleyapp.com",
    "last_seen": "2018-12-26 19:54:26"
}
```

###### How to Get an Access Token
If user is authorized and login is successful, the API will respond with an access token.

## Settings

------------ | -------------
Description | All global settings/options required for reporting
URL | /settings
Method | GET
Parameters | access_token
Request | /settings?access_token=CPrKJK1k51b

###### Response
```
{
    "success": true,
    "title": "Request Successful.",
    "settings": [
        {
            "id": "1",
            "type": "report",
            "meta_key": "1",
            "meta_value": "Near Miss",
            "created": "2018-03-25 08:45:36"
        },
        {
            "id": "2",
            "type": "report",
            "meta_key": "2",
            "meta_value": "Unsafe Act",
            "created": "2018-03-25 08:47:13"
        },
        {
            "id": "3",
            "type": "report",
            "meta_key": "3",
            "meta_value": "Unsafe Conditions",
            "created": "2018-03-25 08:47:45"
        },
        {
            "id": "4",
            "type": "report",
            "meta_key": "4",
            "meta_value": "Stop Card",
            "created": "2018-03-25 08:48:23"
        },
        {
            "id": "5",
            "type": "report",
            "meta_key": "5",
            "meta_value": "Incident",
            "created": "2018-03-25 08:49:22"
        },
        {
            "id": "6",
            "type": "incident",
            "meta_key": "1",
            "meta_value": "Physical Injuries",
            "created": "2018-03-25 09:33:47"
        },
        {
            "id": "7",
            "type": "incident",
            "meta_key": "2",
            "meta_value": "Pollution",
            "created": "2018-03-25 09:34:12"
        },
        {
            "id": "8",
            "type": "incident",
            "meta_key": "3",
            "meta_value": "Material Or Production Related Damages",
            "created": "2018-03-25 09:35:20"
        },
        {
            "id": "9",
            "type": "incident",
            "meta_key": "4",
            "meta_value": "Impact On Public Opinion",
            "created": "2018-03-25 09:36:35"
        },
        {
            "id": "10",
            "type": "severity",
            "meta_key": "1",
            "meta_value": "Minor",
            "created": "2018-03-25 09:44:09"
        } ...
    ]
}
```

## Report

------------ | -------------
Description | Send report to the ReportingAPI Backend Service.
URL | /report
Method | POST

###### Parameters
------------ | -------------
Parameter | Required | Description
id | No | Id for the locally saved report 

###### Response
```
{
    "success": true,
    "title": "Request Successful.",
    "message": "Articles OK.",
    "articles": [
        {
            "id": "jGlpg0DgwDz",
            "title": "Which  safety precautions must be taken when performing maintenance on the system",
            "alias": "which-safety-precautions-must-be-taken-when-performing-maintenance-on-the-system",
            "category": "q4L0VB7krD5",
            "attachment": [
                "attachments/safety-precause.jpg"
            ],
            "precautions": "<p>&nbsp;</p>\r\n<p><strong><em>Always remember to disconnect the PV array</em></strong></p>\r\n<p>&nbsp;</p>\r\n<p><strong><em> from charge controller when checking the system</em></strong></p>",
            "details": [
                "Servicing, Operation and Maintenance logbook must be checked",
                "Personal protective equipment must be worn when needed ",
                "Check digital multimeter with clip-on ammeter ",
                "Check for differential Residual Current Device (RCD) ",
                "Check wire brush",
                "Check Acid neutralising agent ",
                "Check clean cloths ",
                "Check contact grease ",
                "Check clear and clean water without detergent ",
                "Check non-abrasive sponges ",
                "Have a bucket",
                "Check toolbox "
            ],
            "created": "2018-12-11 10:23:51",
            "updated": "2018-12-20 16:45:50"
        }
    ],
    "last_seen": "2018-12-12 23:08:54"
}
```

