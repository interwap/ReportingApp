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

------------ | ------------- | ------------- | -------------
Parameter | Required | Description | Type
id | No | Local report ID | int
access_token | Yes | Access Token | String
type | Yes | Report Type | int
name_of_facility | No | Name Of Facility | String
type_of_facility | No | Type Of Facility | String
area | No | Area | String
cd | No | Circumstance Date | DateTime
md | No | Modified Date | DateTime
nature_of_incident | No | Nature Of Incident | int
sl | No | Severity Level | int
stop_card | No | Stop Card ID| String
sia | No | Stop Card Issued Against | String
sur | No | Stop Card User Role | int
violation | No | Violation | String
consequences | No | Consequences | String
incident_status | No | Incident Status | int
action_taken | No | Immediate Action Taken | String
communication | No | Communication | String
other | No | Other | String
fir | No | Formal Investigation Required | int
attachments | No | Attachments - Comma separated base64 images. Image compression may be required. Large images must be compressed to sizes that can be transmitted with the slowest of internet connection without loosing quality. | String

###### Response
```
{
    "success": true,
    "title": "Request Successful.",
    "id": "10",
    "messages": "Request Successful",
    "reported": "2018-12-27 04:54:56"
}
```

## Errors
```
{
    "success": false,
    "title": "Request Failed.",
    "messages": ["Oops! Something went wrong"]
}
```

##### Developer Notes

**Types of settings**
1. General – Version & Support
2. Facility – Facilities
3. Area - Areas
4. Severity – Report Severity
5. Incident – Incident Types
6. Report – Report Types
7. Rules - Golden Rules

All settings are classified by type, meta_key and meta_value. For the most part, meta_key is mostly numeric.




