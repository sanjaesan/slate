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
<code>Email</code> must be present in the database
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
<code>Email</code> must be present in the database
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

This endpoint reset password. 

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
You can retrieve individual users as well as a list of all `Talent`, `Client` users with the available API.

User Types can be exists in three flavors `Talent`, `Employers` and `Admin`

**Value for the each user type will mean following:**

user Type |  Value 
--------- | ------- 
Talent | 1
Employers | 2
Admin | 3 


## Get a All users

This Endpoint is only available for super users

```shell
curl "https://api.kovatek.com/users" \
  -H "Authorization: Bearer XXXXXXXXXXX"
```
>   

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
    "Verify": "Xx4V7yFm3vc1L6Rrn70EJ_RKv0_E-402X_IDRSIi4xE=",
    "Verified": true,
    "UserType": 1,
    "SuperUser": false
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
    "Verify": "3nroQ3cA90Z_0NnUmMppcSwBeCyIyPIRuYOxjGcXtkY=",
    "Verified": true,
    "UserType": 1,
    "SuperUser": false
  }
]  
```

This endpoint retrieves all User.

### HTTP Request

`GET http://api.kovatek.com/users`

<aside class="notice">
Paginated to <code>100</code> Per request 
</aside>


## Get a Specific user

```shell
curl "https://api.kovatek.com/users/2"
  -H "Authorization: Bearer XXXXXXXXXXX"
```
> Response looks like this

```json
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
    "Verify": "Xx4V7yFm3vc1L6Rrn70EJ_RKv0_E-402X_IDRSIi4xE=",
    "Verified": true,
    "UserType": 1,
    "SuperUser": false
  }  
```

This endpoint retrieves a specific User.

### HTTP Request

`GET http://api.kovatek.com/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to retrieve


## Delete a Specific User

```shell
curl "https://api.kovatek.com/users/2"
  -X DELETE
  -H "Authorization: Token"
```

> The above command returns JSON structured like this:

```json
{
  "message":"204"
}
```

This endpoint deletes a specific user.

### HTTP Request

`DELETE https://api.kovatek.com/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to delete

# Settings

## Get a specified user settings
## Get user Avatar
## Update Profile Settings
## Update Payment Settings
## Update Account Settings
## Update Notification settings

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