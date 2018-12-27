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

## Categories

------------ | -------------
Description | All articles on the CharleyApp Backend Service are grouped into categories. This lets your app fetch all categories a user group has permission to.
URL | /categories
Method | GET
Parameters | access_token
Request | /categories?access_token=CPrKJK1k51b

###### Response
```
{
    "success": true,
    "title": "Request Successful.",
    "message": "Categories OK.",
    "categories": [
        {
            "id": "j6K8JXLJzR5",
            "name": "Solar System Installation",
            "alias": "solar-system-installation",
            "author": "4mDGJ9RVLjn",
            "parent": "5vr3JwXVZXY",
            "attachment": "attachments/4-compressor.jpg",
            "created": "2018-12-11 08:54:54"
        },
        {
            "id": "5LXng2ZgyY7",
            "name": "Usage of Solar System",
            "alias": "usage-of-solar-system",
            "author": "4mDGJ9RVLjn",
            "parent": "5vr3JwXVZXY",
            "attachment": "attachments/solar-compressor.png",
            "created": "2018-12-11 08:57:01"
        },
        {
            "id": "q4L0VB7krD5",
            "name": "Maintenance of Solar System - Preventive or Planned",
            "alias": "maintenance-of-solar-system-preventive-or-planned",
            "author": "4mDGJ9RVLjn",
            "parent": "5vr3JwXVZXY",
            "attachment": "attachments/6-compressor.jpg",
            "created": "2018-12-11 09:00:46"
        }
    ],
    "last_seen": "2018-12-12 21:51:49"
}
```

## Articles

------------ | -------------
Description | All articles on the CharleyApp Backend Service are linked to a parent category. This let's you fetch the articles and url to their accompanying media files.
URL | /articles
Method | GET
Parameters | access_token & category
Request | /articles?access_token=CPrKJK1k51b&category=5vr3JwXVZXY

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

## Password

------------ | -------------
Description | Changing password to CharleyApp account.
URL | /password
Method | POST
Parameters | access_token & password
Hint | password parameter is the new password (string)

###### Response
```
{
    "success": true,
    "title": "Request Successful.",
    "message": "Password Saved.",
    "last_seen": "2018-12-24 22:43:12"
}
```

## Expert

------------ | -------------
Description | Request expert on the CharleyApp Backend Service.
URL | /expert
Method | POST
Parameters | access_token & article
Hint | article parameter is the official article id (string) - e.g bGlpg0DgwDz

###### Response
```
{
    "success": true,
    "title": "Request Successful.",
    "message": "Password Saved.",
    "last_seen": "2018-12-24 22:43:12"
}
```

## Beacon

------------ | -------------
Description | Send a beacon to the CharleyApp Backend Service. This should be sent in the background whenever and article is opened/created in the activity lifecycle. CharleyApp uses this ping for analytical purposes and app usage tracking.
URL | /beacon
Method | POST
Parameters | access_token & article
Hint | article parameter is the official article id (string) - e.g bGlpg0DgwDz

###### Response
```
{
    "success": true,
    "title": "Request Successful.",
    "message": "Beacon Successfully.",
    "last_seen": "2018-12-24 22:52:25"
}
```

## Feedback

------------ | -------------
Description | Send user feedbacks to the CharleyApp Backend Service.
URL | /feedback
Method | POST
Parameters | access_token, name_of_station, name_of_dealer, equipment, description, date_of_anomaly, feedback_on_repairs
Hint | Date Format: d-m-y, all other parameters are of string datatype.

###### Response
```
{
    "success": true,
    "title": "Request Successful.",
    "message": "Feedback Sent.",
    "last_seen": "2018-12-24 22:59:58"
}
```

## Media
All attachments and media files can be accessed via the host url: [troubleshooting.charleyapp.com/](http://troubleshooting.charleyapp.com/)

Accepted media files and are formats are listed below:

------------ | -------------
Images | JPG, PNG
Video | MP4
