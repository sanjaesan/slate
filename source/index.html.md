---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - Kovadocs

includes:
  - errors

search: true
---

# Introduction

Welcome!! This documentation is usefull to know how to interact with the Kovatek API endpoints.

Bindings only exist in Shell!. You can view code examples in the dark area to the right.

# Authentication

## Signup

> To signup, curl this script:

```shell
curl -X POST \
  -H 'Content-Type: application/json' \
  -d '{"email":"Joe@gmail.com", "password":"p4ssw0rd","user_type":1}' \
  "https://api.kovatek.com/signup"
```

> Make sure to replace `Joe@gmail.com` and `P4ssw0rd` with your's repectively.

This endpoint Creates a new user.

### HTTP Request

`POST https://api.kovatek.com/signup`
### Parameters

Parameter | Type | Description
--------- | ------- | -----------
email | string | Email field is required.
password | string | Password must be 8 chars or more.
user_type | integer | Required with value 1,  2,  3.

<aside class="notice">
<code>Email</code> must be unique
</aside>


## Login

> To login, curl this script:

```shell
curl -X POST \
  -H 'Content-Type: application/json' \
  -d '{"email":"Joe@gmail.com", "password":"p4ssw0rd"}' \
  "https://api.kovatek.com/signup"
```

> Make sure to replace `Joe@gmail.com` and `P4ssw0rd` with your's repectively.

This endpoint logs in user.

### HTTP Request

`POST https://api.kovatek.com/login`
### Parameters

Parameter | Type | Description
--------- | ------- | -----------
email | string | Email field is required.
password | string | Password must be 8 chars or more.


<aside class="notice">
<code>Email</code> must be unique
</aside>

## Token

> To Receive email verification token, curl this script:

```shell
curl -X POST \
  -H 'Content-Type: application/json' \
  -d '{"email":"Joe@gmail.com"}' \
  "https://api.kovatek.com/token"
```

> Make sure to replace `Joe@gmail.com` with your email

This endpoint sends verification token to the email provided. This is useful when user couldn't complete 
registration with the above http request

### HTTP Request

`POST https://api.kovatek.com/api/token`

### Parameters

Parameter | Type | Description
--------- | ------- | -----------
email | string | Email field is required.

<aside class="notice">
<code>Email</code> must exists
</aside>

## Verify

> To Verify email, curl this script:

```shell
curl -X POST \
  -H 'Content-Type: application/json' \
  -d '{"token":"XXXXXXXXXXXXXXXX"}' \
  "https://api.kovatek.com/verify"
```

> Make sure to replace `XXXXXXXXXXXXXXXX` with token received

This endpoint verifies user email. 

### HTTP Request

`POST https://api.kovatek.com/api/forget`

### Parameters

Parameter | Type | Description
--------- | ------- | -----------
token | string | Token is required.

<aside class="notice">
<code>Token</code> must be valid
</aside>


## Forget

> To Receive password reset token, curl this script:

```shell
curl -X POST \
  -H 'Content-Type: application/json' \
  -d '{"email":"Joe@gmail.com"}' \
  "https://api.kovatek.com/forget"
```

> Make sure to replace `Joe@gmail.com` with your email

This endpoint sends password reset token to the email provided. 

### HTTP Request

`POST https://api.kovatek.com/forget`

### Parameters

Parameter | Type | Description
--------- | ------- | -----------
email | string | Email field is required.

<aside class="notice">
<code>Email</code> must exists
</aside>

## Reset

> To Receive email verification token, curl this script:

```shell
curl -X POST \
  -H 'Content-Type: application/json' \
  -d '{"token":"XXXXXXXXXXXXX"}' \
  "https://api.kovatek.com/reset"
```

> Make sure to replace `XXXXXXXXXXXXX` with token received 

This endpoint resets password. 

### HTTP Request

`POST https://api.kovatek.com/reset`

### Parameters

Parameter | Type | Description
--------- | ------- | -----------
token | string | token is required.

<aside class="notice">
<code>Token</code> must be valid
</aside>

# Users

The User Objects represent the members with an active kovatek account. 

User Types exists in four flavors `Talent`, `Client`,`Admin` and `Super`

**Value for each user type will mean the following:**

User Type |  Value 
--------- | ------- 
Talent | 1
Client | 2
Admin | 3 
Super | 4

<aside class="notice">
<code>Super</code> users are indeed super, You can't register them
</aside>


## Get user

```shell
curl "https://api.kovatek.com/users/7" \
  -H "Authorization: Bearer XXXXXXXXXXX"
```
> Response

```json
  {
    "ID": 7,
    "CreatedAt": "2020-05-17T21:33:29.395372Z",
    "UpdatedAt": "2020-05-17T21:33:29.395372Z",
    "DeletedAt": null,
    "Email": "me@mail.kovatek.com",
    "KovatekID": "",
    "Password": "",
    "PasswordHash": "$2a$10$mbHS13q/xm94xUS9q/w5GuYGYS2MQs20HMBC0pLsQEYKi1QA1aYQ.",
    "Remember": "",
    "RememberHash": "mb4le2fAPcc_LWAPQEuYHBcuuuj2MlTp_hNCUljnMJw=",
    "Verify": "",
    "Verified": false,
    "UserType": 3
  } 
```
This Endpoint gets a specified user and it's available for all user types hierarchically.

* Talent can retrieve other Talents and clients only
* Clients can retrieve other clients and talents only
* Admin can retrieve other admins, clients and talents only
* Super can retrieve all user types

### HTTP Request

`GET http://api.kovatek.com/users/<ID>`

### URL Parameters

Parameter | Description
--------- | ------- 
ID | The ID of the user to retrieve

## Get All Talents

```shell
curl "https://api.kovatek.com/users/talents?limit=2" \
  -H "Authorization: Bearer XXXXXXXXXXX"
```

> Response

```json
[  
  {
    "ID": 9,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "talent@gmail.com",
    "Password": "",
    "PasswordHash": "$2a$10$Wwp/kFBMAW0AOuZKlxjxseTloyIA3/GlYmbISSN04J5sfeb3IqhUi",
    "Remember": "",
    "RememberHash": "bjTm9yLCv_s0Vb2-udOfxLxy_ClKIhYnuF0uzQrAk5U=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 1,
},
  {
    "ID": 23,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "coder@gmail.com",
    "Password": "",
    "PasswordHash": "$2a$10$eBB6sc7pQrqtBLeeoTieoeN9OcR5L4ORylIGNRUEqyxNml8aIPhYC",
    "Remember": "",
    "RememberHash": "FKs1QvhTOlCf69WYhFFFe9xs9iqKQabdsHOQ2MgzxrE=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 1,
  }
]  
```
This Endpoint is available for all user types and retrieves talents with a limit or offset query

### HTTP Request

`GET http://api.kovatek.com/users/talents`

<aside class="notice">
Default limit is <code>10</code> and default offset is <code>0</code>
</aside>


## Get All Clients

```shell
curl "https://api.kovatek.com/users/clients?limit=2" \
  -H "Authorization: Bearer XXXXXXXXXXX"
```
> Response

```json
[  
  {
    "ID": 1,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "ada@gmail.com",
    "Password": "",
    "PasswordHash": "$2a$10$Wwp/kFBMAW0AOuZKlxjxseTloyIA3/GlYmbISSN04J5sfeb3IqhUi",
    "Remember": "",
    "RememberHash": "bjTm9yLCv_s0Vb2-udOfxLxy_ClKIhYnuF0uzQrAk5U=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 2,
},
  {
    "ID": 2,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "joe@gmail.com",
    "Password": "",
    "PasswordHash": "$2a$10$eBB6sc7pQrqtBLeeoTieoeN9OcR5L4ORylIGNRUEqyxNml8aIPhYC",
    "Remember": "",
    "RememberHash": "FKs1QvhTOlCf69WYhFFFe9xs9iqKQabdsHOQ2MgzxrE=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 2,
  }
]  
```

This Endpoint is available for all user types and retrieves all clients
with a limit or offset query

### HTTP Request

`GET http://api.kovatek.com/users/clients`

<aside class="notice">
Default limit is <code>10</code> and default offset is <code>0</code>
</aside>


## Get All Admins

```shell
curl "https://api.kovatek.com/users/admins?limit=2" \
  -H "Authorization: Bearer XXXXXXXXXXX"
```
> Response

```json
[  
  {
    "ID": 15,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "you@mail.kovatek.com",
    "Password": "",
    "PasswordHash": "$2a$10$Wwp/kFBMAW0AOuZKlxjxseTloyIA3/GlYmbISSN04J5sfeb3IqhUi",
    "Remember": "",
    "RememberHash": "bjTm9yLCv_s0Vb2-udOfxLxy_ClKIhYnuF0uzQrAk5U=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 3,
},
  {
    "ID": 7,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "me@mail.kovatek.com",
    "Password": "",
    "PasswordHash": "$2a$10$eBB6sc7pQrqtBLeeoTieoeN9OcR5L4ORylIGNRUEqyxNml8aIPhYC",
    "Remember": "",
    "RememberHash": "FKs1QvhTOlCf69WYhFFFe9xs9iqKQabdsHOQ2MgzxrE=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 3,
  }
]  
```

This Endpoint is available for admin and super users and retrieves all admins
with a limit or offset query

### HTTP Request

`GET http://api.kovatek.com/users/admins`

<aside class="notice">
Default limit is <code>10</code> and default offset is <code>0</code>
</aside>


## Get All Supers

```shell
curl "https://api.kovatek.com/users/supers?offset=5" \
  -H "Authorization: Bearer XXXXXXXXXXX"
```
> Response

```json
[  
  {
    "ID": 6,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "baba@super.com",
    "Password": "",
    "PasswordHash": "$2a$10$Wwp/kFBMAW0AOuZKlxjxseTloyIA3/GlYmbISSN04J5sfeb3IqhUi",
    "Remember": "",
    "RememberHash": "bjTm9yLCv_s0Vb2-udOfxLxy_ClKIhYnuF0uzQrAk5U=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 4,
},
  {
    "ID": 21,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "super@mail.kovatek.com",
    "Password": "",
    "PasswordHash": "$2a$10$Wwp/kFBMAW0AOuZKlxjxseTloyIA3/GlYmbISSN04J5sfeb3IqhUi",
    "Remember": "",
    "RememberHash": "bjTm9yLCv_s0Vb2-udOfxLxy_ClKIhYnuF0uzQrAk5U=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 4,
},
  {
    "ID": 33,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "boss@mail.kovatek.com",
    "Password": "",
    "PasswordHash": "$2a$10$eBB6sc7pQrqtBLeeoTieoeN9OcR5L4ORylIGNRUEqyxNml8aIPhYC",
    "Remember": "",
    "RememberHash": "FKs1QvhTOlCf69WYhFFFe9xs9iqKQabdsHOQ2MgzxrE=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 4,
  }
]  
```

This Endpoint is available for Super users and retrieves all supers
with a limit or offset query

### HTTP Request

`GET http://api.kovatek.com/users/supers`

<aside class="notice">
Default limit is <code>10</code> and default offset is <code>0</code>
</aside>

## Get All User Types

```shell
curl "https://api.kovatek.com/users/supers?offset=200" \
  -H "Authorization: Bearer XXXXXXXXXXX"
```
> Response

```json
[  
  {
    "ID": 201,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "dev@dev.com",
    "Password": "",
    "PasswordHash": "$2a$10$Wwp/kFBMAW0AOuZKlxjxseTloyIA3/GlYmbISSN04J5sfeb3IqhUi",
    "Remember": "",
    "RememberHash": "bjTm9yLCv_s0Vb2-udOfxLxy_ClKIhYnuF0uzQrAk5U=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 1,
},
  {
    "ID": 202,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "client@client.com",
    "Password": "",
    "PasswordHash": "$2a$10$Wwp/kFBMAW0AOuZKlxjxseTloyIA3/GlYmbISSN04J5sfeb3IqhUi",
    "Remember": "",
    "RememberHash": "bjTm9yLCv_s0Vb2-udOfxLxy_ClKIhYnuF0uzQrAk5U=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 2,
},
  {
    "ID": 203,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "admin@mail.kovatek.com",
    "Password": "",
    "PasswordHash": "$2a$10$Wwp/kFBMAW0AOuZKlxjxseTloyIA3/GlYmbISSN04J5sfeb3IqhUi",
    "Remember": "",
    "RememberHash": "bjTm9yLCv_s0Vb2-udOfxLxy_ClKIhYnuF0uzQrAk5U=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 3,
},
  {
    "ID": 204,
    "CreatedAt": "2020-05-14T12:54:14.03108+01:00",
    "UpdatedAt": "2020-05-14T12:54:14.03108+01:00",
    "DeletedAt": null,
    "Email": "user@super.com",
    "Password": "",
    "PasswordHash": "$2a$10$eBB6sc7pQrqtBLeeoTieoeN9OcR5L4ORylIGNRUEqyxNml8aIPhYC",
    "Remember": "",
    "RememberHash": "FKs1QvhTOlCf69WYhFFFe9xs9iqKQabdsHOQ2MgzxrE=",
    "Verify": "",
    "Verified": true,
    "Locked": false,
    "UserType": 4,
  }
]  
```

This Endpoint is available for only Super users and retrieves all user types
with a limit or offset query

### HTTP Request

`GET http://api.kovatek.com/users/`

<aside class="notice">
Default limit is <code>10</code> and default offset is <code>0</code>
</aside>

## Update User Password

```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{"old_password":"XXXXXXXXX", "new_password":"#########"}' \
    "https://api.kovatek.com/users/2" 

```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to update users password

### HTTP Request

`GET http://api.kovatek.com/users/<ID>`

### URL Parameters

Parameter | Description
--------- | ------- 
ID | The ID of the user to update


## Delete a Specific User

```shell
curl "https://api.kovatek.com/users/2" \
  -X DELETE \
  -H "Authorization: Bearer XXXXXXXXXXX"
```

> Response

```json
{
  "message":"204"
}
```

This endpoint is available only for the user himself, 
why would you want to delete someone else's account? lol.
Super users can do that also anyways.

### HTTP Request

`DELETE https://api.kovatek.com/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to delete

# Settings
The Setting Objects holds members profile, account and payment info.

## Get Avatar

```shell
curl "https://api.kovatek.com/settings/7/avatar" \
  -H "Authorization: Bearer XXXXXXXXXXX"
```
> Response

```json
  {

  } 
```
This Endpoint gets a specified user avatar, you can only get what you own
### HTTP Request

`GET http://api.kovatek.com/settings/<ID>/avatar`

### URL Parameters

Parameter | Description
--------- | ------- 
ID | The ID of the user to retrieve avatar

## Get setting

```shell
curl "https://api.kovatek.com/settings/32442" \
  -H "Authorization: Bearer XXXXXXXXXXX"
```
> Response

```json
  {
    "ID": 32442,
    "CreatedAt": "2020-05-17T22:04:20.993888Z",
    "UpdatedAt": "2020-05-17T22:24:43.84589Z",
    "DeletedAt": null,
    "UserID": 32442,
    "Avatar": "pics.png",
    "Email": "me@mail.kovatek.com",
    "Firstname": "Adama",
    "Surname": "Traore",
    "Phone": "0801000000",
    "City": "Abuja",
    "Country": "Nigeria",
    "Skills": ["docker","CICD","Python","Vuejs"],
    "AccountName": "Adama Traore",
    "AccountNumber": 2060000206,
    "BankName": "UBA",
    "Language": "English",
    "Currency": "NGN",
    "InviteLink": "https://kovatek.com/invite/4f43f34",
    "EmailNewsletter": true,
    "EmailPaymentReceipt": false,
    "EmailNewProjectUploaded": true,
    "EmailMilestoneApproved": false,
    "EmailNewMemberAdded": false
  } 
```
This Endpoint gets a specified user settings and it's available for all user types hierarchically.

* Talent can retrieve other Talents and clients only
* Clients can retrieve other clients and talents only
* Admin can retrieve other admins, clients and talents only
* Super can retrieve all user types

### HTTP Request

`GET http://api.kovatek.com/settings/<ID>`

### URL Parameters

Parameter | Description
--------- | ------- 
ID | The ID of the user to retrieve it's setting

## Get all settings


```shell
curl "https://api.kovatek.com/settings/?offset=32442" \
  -H "Authorization: Bearer XXXXXXXXXXX"
```
> Response

```json
  [
    {
      "ID": 32442,
      "CreatedAt": "2020-05-17T22:04:20.993888Z",
      "UpdatedAt": "2020-05-17T22:24:43.84589Z",
      "DeletedAt": null,
      "UserID": 32442,
      "Avatar": "pics.png",
      "Email": "me@mail.kovatek.com",
      "Firstname": "Adama",
      "Surname": "Traore",
      "Phone": "0801000000",
      "City": "Abuja",
      "Country": "Nigeria",
      "Skills": ["docker","CICD","Python","Vuejs"],
      "AccountName": "Adama Traore",
      "AccountNumber": 2060000206,
      "BankName": "UBA",
      "Language": "English",
      "Currency": "NGN",
      "InviteLink": "https://kovatek.com/invite/4f43f34",
      "EmailNewsletter": true,
      "EmailPaymentReceipt": false,
      "EmailNewProjectUploaded": true,
      "EmailMilestoneApproved": false,
      "EmailNewMemberAdded": false
    },
    {
      "ID": 32443,
      "CreatedAt": "2020-05-17T22:04:20.993888Z",
      "UpdatedAt": "2020-05-17T22:24:43.84589Z",
      "DeletedAt": null,
      "UserID": 32443,
      "Avatar": "deji.png",
      "Email": "me@dev.com",
      "Firstname": "Adelowo",
      "Surname": "Adedeji",
      "Phone": "0909000000",
      "City": "Lagos",
      "Country": "Nigeria",
      "Skills": ["Kubernetes","CICD","Docker","Jenkins"],
      "AccountName": "Adelowo Adedeji",
      "AccountNumber": 3060000306,
      "BankName": "FirstBank",
      "Language": "English",
      "Currency": "NGN",
      "InviteLink": "https://kovatek.com/invite/53t3540",
      "EmailNewsletter": true,
      "EmailPaymentReceipt": false,
      "EmailNewProjectUploaded": true,
      "EmailMilestoneApproved": false,
      "EmailNewMemberAdded": false
    } 
  ]
```
This Endpoint gets all user settings, available for admin and supers
### HTTP Request

`GET http://api.kovatek.com/settings/`


## Update Profile Setting
```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{"firstname": "Adelowo", 
         "furname": "Adedeji",
         "phone": "0909000000",
         "city": "Lagos",
         "country": "Nigeria",
         "skills": ["Kubernetes","CICD","Docker","Jenkins"]
        }' \
    "https://api.kovatek.com/settings/32423/profile" 
```
> Response

```json
{
  "200": "Success"
} 
```

This Endpoint is available to update user profile settings

### HTTP Request
`GET http://api.kovatek.com/settings/<ID>/profile`


### URL Parameters

Parameter | Description
--------- | ------- 
ID | The ID of the user to update it's profile settings



## Update Payment Setting

```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{"account_name": "Adedeji Adelowo",
         "account_number": 3060000306,
         "bank_name": "FirstBank",
        }' \
    "https://api.kovatek.com/settings/32423/payment" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to update user payment setting

### HTTP Request

`GET http://api.kovatek.com/settings/<ID>/payment`

### URL Parameters

Parameter | Description
--------- | ------- 
ID | The ID of the user to update it's payment setting

## Update Account Setting

```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{"language": "English",
         "currency": "NGN",
        }' \
    "https://api.kovatek.com/settings/32423/account" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to update user account setting

### HTTP Request

`GET http://api.kovatek.com/settings/<ID>/account`

### URL Parameters

Parameter | Description
--------- | ------- 
ID | The ID of the user to update it's account setting

## Update Notification setting
```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{"email_newsletter": true,
         "email_payment_receipt": false,
         "email_new_project_uploaded": true,
         "email_milestone_approved": false,
         "email_new_member_added": true
        }' \
    "https://api.kovatek.com/settings/32423/notification" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to update user notification setting

### HTTP Request

`GET http://api.kovatek.com/settings/<ID>/notification`

### URL Parameters

Parameter | Description
--------- | ------- 
ID | The ID of the user to update it's notification setting

# Projects

## Create a New Project
## Create Milestone for a Project
## Get a specified Project
## Get all Projects
## Onboard Talents for a Specific Project
## Update a Project Milestone
## Update Project


# Test

## Take a Test
## Get a specific Test
## Get all Tests
## Update Test
## Delete Test

# Question

## Create a Question
## Get a Questiom
## Get all Question
## Update Question
## Delete Question

# Grade

## Grade a Test
## Get all Grades
## Update Grade
## Delete Grade

# Interview

## Create an Interview
## Get all Interviews