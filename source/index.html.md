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
    "Email": "coder@gmail.com",
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
ID | The ID of the user to retrieve its setting

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
      "Email": "coder@gmail.com",
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


# Profiles
The Profile Objects holds profile data.

**Talents Seniority Level**

Level |  Value 
--------- | ------- 
Junior | 1
Intermediate | 2
Senior | 3 


## Get Talents Profile

```shell
curl "https://api.kovatek.com/talents/profiles" \
  -H "Authorization: Bearer XXXXXXXXXXX"
```
> Response

```json
  {
    "ID": 2132,
    "CreatedAt": "2020-05-31T09:39:23.548454+01:00",
    "UpdatedAt": "2020-05-31T09:39:23.548454+01:00",
    "DeletedAt": null,
    "UserID": 2132,
    "Title": "Web Developer",
    "AboutMe": "I am a backend developer with more than 7 years experience on web development. My excellent knowledge includes:",
    "MoreDetails": "I am problem solving, eager to learn new things if needed, Does Something works for you? Let's get in touch.",
    "SeniorityLevel": 2,
    "ProjectsCompleted": 4,
    "ProjectsLeaded": 0,
    "RemoteJobsCompleted": 0,
    "WorkRate": 30,
    "SkillScore": 0,
    "TotalTests": 0,
    "Reviews": 0,
    "WorkExperience": 7,
    "Interviews": 0,
    "CurrentlyHired": false,
    "ScheduleInterview": null,
    "City":"",
    "Country":"",
    "Skills":["Golang","Ruby"]
  } 
```
This Endpoint gets a specified talent profile
### HTTP Request

`GET http://api.kovatek.com/talents/profiles/search`

### URL Parameters

Parameter | Description
--------- | ------- 
ID | The ID of the talent to retrieve profile

## Get Clients Profile

```shell
curl "https://api.kovatek.com/clients/profiles" \
  -H "Authorization: Bearer XXXXXXXXXXX"
```
> Response

```json
  {
    "ID": 532,
    "CreatedAt": "2020-05-31T09:39:23.548454+01:00",
    "UpdatedAt": "2020-05-31T09:39:23.548454+01:00",
    "DeletedAt": null,
    "ClientID": 532,
    "ProjectsPosted": 5,
    "AmountSpent": 10000
  } 
```
This Endpoint gets a specified talent profile
### HTTP Request

`GET http://api.kovatek.com/clients/profile`

### URL Parameters

Parameter | Description
--------- | ------- 
ID | The ID of the client to retrieve profile

## Browse Talents
```shell
curl -X POST \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{
         "Title": "Web Developer",
         "seniority_level": 2,
         "work_rate": 15,
         "work_experience": 7
        }' \
    "https://api.kovatek.com/talents/profiles/search?offset=0&limit=10" 
```
> Response

```json
{
  [

  ]
} 
```

This Endpoint is available to browse talent profile with optional filters

### HTTP Request

`POST http://api.kovatek.com/talents/profiles/search`

### Optional Filter Parameters

Parameter | Description
--------- | ------- 
Title| Returns profiles that matches value
City | Returns profiles that matches value
Country| Returns profiles that matches value
SeniorityLevel | Returns profiles that are >= value provided
WorkExperience | Returns profiles that are >= value provided
WorkRate | Returns profiles that are <= value provided
Skills | Returns profiles that matches members of the slice provided



<aside class="notice">
Passing <code>Zero Values</code> for all parameters will return all talents unfiltered
</aside>

## Edit Talents Profile
```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{
         "Title": "Web Developer",
         "about_me": "I am a backend developer with more than 7 years experience on web development. My excellent knowledge includes:",
         "seniority_level": 2,
         "more_details": "I am problem solving, eager to learn new things if needed, Does Something works for you? Let us get in touch.",
         "work_experience": 7
        }' \
    "https://api.kovatek.com/talents/profiles" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to Update talent profile

### HTTP Request

`PUT http://api.kovatek.com/clients/profiles/:id`

## Edit Clients Profile
```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{
         
        }' \
    "https://api.kovatek.com/clients/profiles" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to Update client profile

### HTTP Request

`PUT http://api.kovatek.com/clients/profiles`

# Projects

Fields | Type | Required | Description 
--------- | ---- | :------:| -----------
title | string | true | A short project title.
description | string | true | detailed project description.
talent_size | integer | false | max number of developers to onboard.
skills | Array | true | technical requirements.
duration | integer | true|  expressed in days
ongoing | bool | false | to specify if it's a new project
Type | integer | true | to specify if remote, office or crowdsource
complexity | integer| true | complexity of the project
commitment | integer| true | to specify if fixed or hourly
start_budget | float | true | minimum budgeted for the project
end_budget | float | true | maximum budgeted for the project

**Project Duration**

Duration |  Value
--------- | :-------:
OneMonth | 1
ThreeMonths | 2
SixMonths | 3
Undefined | 4


**Project Complexity**        

Complexity |  Value    
--------- | :-----:    
Easy | 1               
Medium | 2
Difficult | 3 

**Project Type**        

Type |  Value    
--------- | :-----:    
Remote | 1               
Office | 2
CrowdSource | 3 

**Project Commitment**        

Commitment |  Value    
--------- | :---:    
Hourly | 1               
Fixed | 2


**Project Status**   

Status |  Value
--------- | :---:  
Created | 1  
Hiring | 2
Closed | 3  
Ongoing | 4
Archived | 5
Completed | 6

## New Project
```shell
curl -X POST \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{"title": "JB Finance",
         "description": "A Fintech project that connect banks to logistic company",
         "talent_size": 5,
         "skills":["Reactjs, "Nodejs", "Grpc", "Protobuf"],
         "type": 1,
         "duration":4,
         "commitment":2,
         "complexity":1,
         "start_budget":3000,
         "end_budget":5000
        }' \
    "https://api.kovatek.com/projects" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to Create New project

### HTTP Request

`POST http://api.kovatek.com/projects`

<aside class="notice">
Only <code>Client</code> user can create a <code>Project</code>
</aside>

## Update Project
```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{
         "description": "A Fintech project that connect banks to logistic company",
         "talent_size": 5,
         "skills":["Sveltejs, "Haskell", "Grpc", "Protobuf"],
         "duration":3
        }' \
    "https://api.kovatek.com/projects/1213" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to Update created projects

### HTTP Request

`PUT http://api.kovatek.com/projects/:id`

<aside class="notice">
All fields except <code>title</code> are updateable
</aside>

## Update Project Status
```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    "https://api.kovatek.com/projects/status/1213?status=5" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to Update projects status

### HTTP Request

`PUT http://api.kovatek.com/projects/status/:id`

## Get Project
```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    "https://api.kovatek.com/projects/1213" 
```
> Response

```json
{  
  "ID": 1213,
  "CreatedAt": "2020-05-26T05:18:32.142905+01:00",
  "UpdatedAt": "2020-05-26T05:28:49.409624+01:00",
  "DeletedAt": null,
  "Title": "JB finance",
  "Description": "A project",
  "ClientID": 1342,
  "type": 1,
  "Duration": 95,
  "Complexity": 0,
  "Status": 0,
  "TalentSize": 5,
  "StartBudget": 500,
  "EndBudget":750
  "Skills":[
    "Sveltejs",
    "Haskell",
    "Grpc",
    "Protobuf"
    ]
} 
```

This Endpoint is available for clients to retrieve specific project

### HTTP Request

`GET http://api.kovatek.com/projects/:id`


## View Projects
```shell
curl -X GET \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    "https://api.kovatek.com/projects/view?limit=1&offset=0" 
```
> Response

```json
{  
  "ID": 1213,
  "CreatedAt": "2020-05-26T05:18:32.142905+01:00",
  "UpdatedAt": "2020-05-26T05:28:49.409624+01:00",
  "DeletedAt": null,
  "Title": "JB finance",
  "Description": "A project",
  "ClientID": 1342,
  "type": 1,
  "Duration": 95,
  "Complexity": 0,
  "Status": 0,
  "TalentSize": 5,
  "StartBudget": 500,
  "EndBudget":750
  "Skills":[
    "Sveltejs",
    "Haskell",
    "Grpc",
    "Protobuf"
    ]
} 
```

This Endpoint is available for talents to see all projects available

### HTTP Request

`GET http://api.kovatek.com/projects/view`


## Get Projects
```shell
curl -H "Authorization: Bearer XXXXXXXXXXX" \
    "https://api.kovatek.com/projects?offset=2&limit=50" 
```
> Response

```json
[  
  {
    "ID": 1213,
    "CreatedAt": "2020-05-26T05:18:32.142905+01:00",
    "UpdatedAt": "2020-05-26T05:28:49.409624+01:00",
    "DeletedAt": null,
    "Title": "Fintech",
    "Description": "A Fintech project that connects banks to logistics company",
    "ClientID": 1342,
    "type": 1,
    "Duration": 95,
    "Complexity": 0,
    "Status": 0,
    "TalentSize": 5,
    "PaymentAmount": 0,
    "Skills":[
      "Sveltejs",
      "Haskell",
      "Grpc",
      "Protobuf"
      ]
  },
  {
    "ID": 1382,
    "CreatedAt": "2020-05-26T05:18:32.142905+01:00",
    "UpdatedAt": "2020-05-26T05:28:49.409624+01:00",
    "DeletedAt": null,
    "Title": "AR/VR Project",
    "Description": "A VR project ....",
    "ClientID": 1342,
    "type": 1,
    "Duration": 95,
    "Complexity": 0,
    "Status": 0,
    "TalentSize": 8,
    "PaymentAmount": 0,
    "Skills":[
      "Unity",
      "C++",
      "Computer Graphics",
      "GluonCV"
      ]
  },
  {
    "ID": 1503,
    "CreatedAt": "2020-05-26T05:18:32.142905+01:00",
    "UpdatedAt": "2020-05-26T05:28:49.409624+01:00",
    "DeletedAt": null,
    "Title": "Ehailing Platform",
    "Description": "A Distibuted & Decentralised Ehailing System",
    "ClientID": 1342,
    "type": 1,
    "Duration": 100,
    "Complexity": 0,
    "Status": 0,
    "TalentSize": 10,
    "PaymentAmount": 0,
    "Skills":[
      "Blockchain",
      "Truffle",
      "Open Zeppellin"
      "Ganache"
      "Solidity",
      "Serpent",
      "LLL",
      "Hyperledger"
      ]
  },
]
```

This Endpoint is available for clients to retrieve all projects

### HTTP Request

`GET http://api.kovatek.com/projects`

## Delete Project
```shell
curl "https://api.kovatek.com/projects/1382" \
  -X DELETE \
  -H "Authorization: Bearer XXXXXXXXXXX"
```

> Response

```json
{
  "message":"204"
}
```

This Endpoint is available to remove a Project by an admin or super user 

### HTTP Request

`DELETE https://api.kovatek.com/projects/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the project to delete

## Browse Projects
```shell
curl -X POST \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{
         "duration": 2,
         "type": 1,
         "commitment": 3,
         "status": 2
         "start_budget": 750 ,
         "complexity": 1
        }' \
    "https://api.kovatek.com/projects/search?offset=0&limit=10" 
```
> Response

```json
{
  [

  ]
} 
```

This Endpoint is available to browse projects with optional filters

### HTTP Request

`POST http://api.kovatek.com/projects/search`

### Optional Filter Parameters

Parameter | Description
--------- | ------- 
Duration| Returns projects that matches value
Commitment | Returns projects that matches value
Complexity | Returns projects that matches value
Type | Returns projects that mathes value
Status | value defaulted to projects in created and hiring status
StartBudget | Returns projects that are >= value provided
Skills | Returns projects that matches members of the slice provided

<aside class="notice">
Passing <code>Zero Values</code> for all parameters will return all projects unfiltered
</aside>


## New Project Bidding 
```shell
curl -X POST \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{"cover_letter": "My cover letter, bidding for project JB finance",
         "delivery_time": 60,
         "milestones": [
           {
             "title": "Login Setup",
             "amount": 300,
             "due_date": "Monday, 20th of January, 2020"
           },
           {
             "title": "API Integration",
             "amount": 89,
             "due_date": "Monday, 20th of January, 2020"
           },
           {
             "title": "Front End",
             "amount": 400,
             "due_date": "Monday, 20th of January, 2020"
           }
         ]
        }' \
    "https://api.kovatek.com/projects/1213/biddings" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available for talents to Create a new bidding for a project

### HTTP Request

`POST http://api.kovatek.com/project/<id>/biddings`

## Update Project Bidding
```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{
         "cover_letter": "My cover letter, bidding for project JB finance",
         "delivery_time": 60
        }' \
    "https://api.kovatek.com/projects/1213/biddings/111" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to Update project Biddings

### HTTP Request

`PUT http://api.kovatek.com/projects/:id/biddings/:idd`


## Get Project Biddings
```shell
curl -H "Authorization: Bearer XXXXXXXXXXX" \
    "https://api.kovatek.com/projects/1213/biddings" 
```
> Response

```json
[  
  {
    "ID": 111,
    "CreatedAt": "2020-06-01T19:26:02.914206+01:00",
    "UpdatedAt": "2020-06-01T20:10:13.869743+01:00",
    "DeletedAt": null,
    "ProjectID": 1213,
    "TalentID": 577,
    "CoverLetter": "My cover letter, bidding for project JB finance",
    "BillAmount": 1250,
    "DeliveryDays": 60,
    "Milestones":
    [
      {
        "ID": 9543,
        "CreatedAt": "2020-06-01T19:26:02.960457+01:00",
        "UpdatedAt": "2020-06-01T19:26:02.960457+01:00",
        "DeletedAt": null,
        "ProjectID": 1213,
        "BiddingID": 111,
        "Title": "Login Setup",
        "Amount": 300,
        "Due": "Monday, 20th of January, 2020"
      },
      {
        "ID": 9544,
        "CreatedAt": "2020-06-01T19:26:02.969782+01:00",
        "UpdatedAt": "2020-06-01T19:26:02.969782+01:00",
        "DeletedAt": null,
        "ProjectID": 1213,
        "BiddingID": 111,
        "Title": "API Integration",
        "Amount": 89,
        "Due": "Monday, 20th of January, 2020"
      },
      {
        "ID": 9545,
        "CreatedAt": "2020-06-01T19:26:02.977086+01:00",
        "UpdatedAt": "2020-06-01T19:26:02.977086+01:00",
        "DeletedAt": null,
        "ProjectID": 1213,
        "BiddingID": 111,
        "Title": "Front End",
        "Amount": 400,
        "Due": "Monday, 20th of January, 2020"
      }
    ]
  }
]
```

This Endpoint is available for clients to retrieve all biddings available for a specified project

### HTTP Request

`GET http://api.kovatek.com/projects/:id/biddings`

## New Project Milestone 
```shell
curl -X POST \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{"milestones": 
          [
           {
             "title": "Signup Setup",
             "amount": 300,
             "due_date": "Monday, 20th of January, 2020"
           },
           {
             "title": "Xcode Integration",
             "amount": 89,
             "due_date": "Monday, 20th of January, 2020"
           },
           {
             "title": "Database",
             "amount": 400,
             "due_date": "Monday, 20th of January, 2020"
           }
          ]
        }' \
    "https://api.kovatek.com/projects/1213/biddings/111/milestones" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available for talents to Create new milestones for a project bidding

### HTTP Request

`POST http://api.kovatek.com/project/<id>/biddings/<id>/milestones`

## Update Project Miilestone
```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{
         "title": "Selenium WebTesting",
         "amount": 1250,
         "due_date": "Monday, 20th of January, 2020"
        }' \
    "https://api.kovatek.com/projects/1213/biddings/111/milestones/892" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to update project milestones

### HTTP Request

`PUT http://api.kovatek.com/projects/:id/biddings/:id/milestones/:id`

<!-- <aside class="notice">
<code>Milestones</code> array fails to update currently 
</aside> -->

## Onboard Talents for a Project

```shell
curl -X POST \
    -H "Authorization: Bearer XXXXXXXXXXX" 
    "https://api.kovatek.com/projects/1213/onboard?talent_id=<ID>" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to onboard talents for a project

### HTTP Request

`POST http://api.kovatek.com/projects/<id>/onboard`

## New Project Task
```shell
curl -X POST \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{"title": "Fintech Task 1",
         "description": "Design a mockup/prototype ......",
         "duration":1.5
        }' \
    "https://api.kovatek.com/projects/1213/tasks" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to Create a new task for project

### HTTP Request

`POST http://api.kovatek.com/project/<id>/tasks`


## Update Project Task
```shell
curl -X PUT \
    -H "Authorization: Bearer XXXXXXXXXXX" \
    -d '{
         "description": "Design a mockup/prototype for AdobeXD ....",
         "duration":2.0
        }' \
    "https://api.kovatek.com/projects/1213/tasks/1243" 
```
> Response

```json
{
  "200": "success"
} 
```

This Endpoint is available to Update project Tasks

### HTTP Request

`PUT http://api.kovatek.com/projects/:id/tasks/:id`


## Get Project Tasks
```shell
curl -H "Authorization: Bearer XXXXXXXXXXX" \
    "https://api.kovatek.com/projects/1213/tasks?offset=2&limit=50" 
```
> Response

```json
[  
  
  {
    "ID": 193,
    "CreatedAt": "2020-05-26T09:49:51.275097+01:00",
    "UpdatedAt": "2020-05-26T09:49:51.275097+01:00",
    "DeletedAt": null,
    "ProjectID": 1213,
    "Title": "Fintech Task 1",
    "Description": "Design a mockup/prototype for AdobeXD",
    "Duration": 2.0
    },
    {
    "ID": 3134,
    "CreatedAt": "2020-05-26T09:50:07.268814+01:00",
    "UpdatedAt": "2020-05-26T09:53:23.821169+01:00",
    "DeletedAt": null,
    "ProjectID": 1213,
    "Title": "Fintech Task 2",
    "Description": "Convert UI mockups into front-end using sveltejs",
    "Duration": 15
    },
    {
    "ID": 3136,
    "CreatedAt": "2020-05-26T09:51:20.23034+01:00",
    "UpdatedAt": "2020-05-26T09:51:20.23034+01:00",
    "DeletedAt": null,
    "ProjectID": 1213,
    "Title": "Fintech Task 3",
    "Description": "Write Integration Tests for your sveltejs components",
    "Duration": 2.5
    },
    {
    "ID": 5456,
    "CreatedAt": "2020-05-26T13:00:00.835402+01:00",
    "UpdatedAt": "2020-05-26T19:57:51.302944+01:00",
    "DeletedAt": null,
    "ProjectID": 1213,
    "Title": "Fintech Task 4",
    "Description": "Integrating Backend API's",
    "Duration": 20
  }
]
```

This Endpoint is available for retrieving project tasks

### HTTP Request

`GET http://api.kovatek.com/projects/:id/tasks`
  

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
## Update Interview
## Get interview
## Get all Interviews