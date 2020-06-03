---
title: Co-Life API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Co-Life API! Co-Life is an app focused on offering co-living opportunities. Through this API you can create and manage your account, your ads and your favorite list. In this guide you can check how to use our endpoints with the help of sample code offered on the right section.

# Authentication

> To authorize, use this code:

```shell
curl "api_endpoint_here"
  -H "X-User-Email: example@testdomain.com"
  -H "X-User-Token: <authentication_token>"
```

> Make sure to replace `authentication_token` with your authentication token.

Co-Life requires your authentication token and email for every request on private end points. They should be included on the header of every request made to the server, in the following format:

`X-User-Email: example@testdomain.com`

`X-User-Token: <authentication_token>`

<aside class="notice">
You must replace <code>authentication_token</code> with your personal authentication token.
</aside>

This app has special features for administrators. In case you want to try them out, use the following credentials on your requests:

`X-User-Email: admin@admin.com`

`X-User-Token: kxdSCt9xFzmxU9HayygE`

# Users

## Sign Up

```shell
curl https://co-life.herokuapp.com/users
  -X POST
  -H "Content-Type: application/json"
  -d '{
    "user":{
      "name": "Example",
      "email": "example@testdomain.com", 
      "password": "example", 
      "password_confirmation": "example"
    }
  }'
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Example",
    "admin": false,
    "email": "example@testdomain.com",
    "created_at": "<current time>",
    "updated_at": "<current time>",
    "authentication_token": "<random token>"
  }
]
```

Creates an account.

<aside class="warning">Don't forget to store your authentication token after this operation!</aside>
<aside class="notice">A user can't become an admin through HTTP requests.</aside>

### HTTP Request

`POST https://co-life.herokuapp.com/users`

Successfull HTTP response: `201 Created`

### Query Parameters

Parameter | Description
--------- | -----------
name | The account's user name
email | The account's email
password | The account's password
password_confirmation | Password confirmation

## Update

```shell
curl https://co-life.herokuapp.com/users/1
  -X PUT
  -H "Content-Type: application/json"
  -H "X-User-Email: example@testdomain.com"
  -H "X-User-Token: <authentication_token>"
  -d '{
    "user":{
      "name": "A Brand New Name"
    }
  }'
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "A Brand New Name",
    "admin": false,
    "email": "example@testdomain.com",
    "created_at": "<creation time>",
    "updated_at": "<current time>",
    "authentication_token": "<random token>"
  }
]
```

Updates an account's information.

<aside class="warning">Only the owner of the account can change its information.</aside>

### HTTP Request

`POST https://co-life.herokuapp.com/users/:id`

Successfull HTTP response: `200 OK`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The id of the account you want to change

### Query Parameters

Parameter | Description
--------- | -----------
name | The account's new user name
email | The account's new email

<aside class="success">Inform only the parameters you want to change!</aside>

## Show

```shell
curl https://co-life.herokuapp.com/users/1
  -X GET
  -H "X-User-Email: example@testdomain.com"
  -H "X-User-Token: <authentication_token>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Example",
    "admin": false,
    "email": "example@testdomain.com",
    "created_at": "<creation time>",
    "updated_at": "<update time>",
    "authentication_token": "<authentication_token>"
  }
]
```

Retrieves information from one account.

<aside class="notice">Common users can check their own data, while admins can also check data of other users, except for their authentication tokens.</aside>

### HTTP Request

`GET https://co-life.herokuapp.com/users/:id`

Successfull HTTP response: `200 OK`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The id of the user you want to check

## Index

```shell
curl https://co-life.herokuapp.com/users
  -X GET
  -H "X-User-Email: example@testdomain.com"
  -H "X-User-Token: <authentication_token>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Example",
    "admin": false,
    "email": "example@testdomain.com",
    "created_at": "<creation time>",
    "updated_at": "<update time>",
    "authentication_token": "<authentication_token>"
  },
  ...,
  {
    "id": 30,
    "name": "Example30",
    "admin": false,
    "email": "example30@testdomain.com",
    "created_at": "<creation time>",
    "updated_at": "<update time>",
    "authentication_token": "<authentication_token>"
  }
]
```

Retrieves information from all accounts, except for their authentication tokens.

<aside class="notice">This action is available only for admins.</aside>

### HTTP Request

`GET https://co-life.herokuapp.com/users`

## Destroy

```shell
curl https://co-life.herokuapp.com/users/1
  -X DELETE
  -H "X-User-Email: example@testdomain.com"
  -H "X-User-Token: <authentication_token>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "User deleted!"
  }
]
```

Deletes one account.

<aside class="notice">Common users can only delete their own accounts. Admins can delete any common accounts. No admin account can be deleted through HTTP requests.</aside>

### HTTP Request

`DELETE https://co-life.herokuapp.com/users/:id`

Successfull HTTP response: `200 OK`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The id of the user you want to delete

# Homes

## Create

```shell
curl https://co-life.herokuapp.com/api/v1/homes 
  -X POST 
  -H "Content-Type: application/json" 
  -H "X-User-Email: example@testdomain.com" 
  -H "X-User-Token: <authentication_token>" 
  -d '{
    "home":{
      "title": "Test Title", 
      "address": "Test St. 404", 
      "city": "Utopolis", 
      "country": "Narnia", 
      "rent": "195.21", 
      "room_type": "shared", 
      "more_info": "Cosy place full of nice ppl! Join us!"
    }
  }'
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "title": "Test Title",
    "address": "Test St. 404",
    "city": "Utopolis",
    "country": "Narnia",
    "rent": "195.21",
    "room_type": "shared",
    "more_info": "Cosy place full of nice ppl! Join us!",
    "user_id": 1,
    "created_at": "<current time>",
    "updated_at": "<current time>",
  }
]
```

Creates a home ad.

### HTTP Request

`POST https://co-life.herokuapp.com/api/v1/homes`

Successfull HTTP response: `201 Created`

### Query Parameters

Parameter | Description
--------- | -----------
title | The title of your ad
address | The address of the home advertised
city | The city of the home advertised
country | The country of the home advertised
rent | How much is the monthly rent of the home advertised 
room_type | Tells if the room advertised is "shared" or "individual" (for one person) 
more_info | Additional information about the room and home

## Show

```shell
curl https://co-life.herokuapp.com/api/v1/homes/1 
  -X GET 
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "title": "Test Title",
    "address": "Test St. 404",
    "city": "Utopolis",
    "country": "Narnia",
    "rent": "195.21",
    "room_type": "shared",
    "more_info": "Cosy place full of nice ppl! Join us!",
    "user_id": 1,
    "created_at": "<creation time>",
    "updated_at": "<update time>",
  }
]
```

Shows information about a home ad.

<aside class="success">This action doesn't require an authentication token!</aside>

### HTTP Request

`GET https://co-life.herokuapp.com/api/v1/homes/:id`

Successfull HTTP response: `200 OK`

### Query Parameters

Parameter | Description
--------- | -----------
ID | The id of the ad you want to check

## Index

```shell
curl https://co-life.herokuapp.com/api/v1/homes 
  -X GET 
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "title": "Test Title",
    "address": "Test St. 404",
    "city": "Utopolis",
    "country": "Narnia",
    "rent": "195.21",
    "room_type": "shared",
    "more_info": "Cosy place full of nice ppl! Join us!",
    "user_id": 1,
    "created_at": "<creation time>",
    "updated_at": "<update time>",
  },
  ... ,
  {
    "id": 37,
    "title": "Another Test Title",
    "address": "Test Av. 200",
    "city": "Distopolis",
    "country": "Mordor",
    "rent": "8195.21",
    "room_type": "individual",
    "more_info": "It's basically hunger games glorified.",
    "user_id": 6,
    "created_at": "<creation time>",
    "updated_at": "<update time>",
  }
]
```

Shows a list of all home ads.

<aside class="success">This action doesn't require an authentication token!</aside>

### HTTP Request

`GET https://co-life.herokuapp.com/api/v1/homes`

Successfull HTTP response: `200 OK`

## Update

```shell
curl https://co-life.herokuapp.com/api/v1/homes/1
  -X PUT 
  -H "Content-Type: application/json" 
  -H "X-User-Email: example@testdomain.com" 
  -H "X-User-Token: <authentication_token>" 
  -d '{
    "home":{
      "title": "Brand New Title"
    }
  }'
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "title": "Brand New Title",
    "address": "Test St. 404",
    "city": "Utopolis",
    "country": "Narnia",
    "rent": "195.21",
    "room_type": "shared",
    "more_info": "Cosy place full of nice ppl! Join us!",
    "user_id": 1,
    "created_at": "<creation time>",
    "updated_at": "<current time>",
  }
]
```

Updates a home ad's information.

<aside class="notice">Users can only update their own ads. Admins can update any ad.</aside>

### HTTP Request

`PUT https://co-life.herokuapp.com/api/v1/homes/:id`

Successfull HTTP response: `200 OK`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The id of the ad you want to update

### Query Parameters

Parameter | Description
--------- | -----------
title | The updated title of the home advertised
address | The updated address of the home advertised
city | The updated city of the home advertised
country | The updated country of the home advertised
rent | The updated rent of the home advertised 
room_type | The updated type of the room offered 
more_info | Updated additional information about the room and home

<aside class="success">Inform only the parameters you want to change!</aside>

## Destroy

```shell
curl https://co-life.herokuapp.com/api/v1/homes/1
  -X DELETE 
  -H "X-User-Email: example@testdomain.com" 
  -H "X-User-Token: <authentication_token>" 
```

> The above command returns JSON structured like this:

```json
[
  {
    "Ad deleted!"
  }
]
```

Deletes a home ad.

<aside class="notice">Users can only delete their own ads. Admins can delete any ad.</aside>

### HTTP Request

`DELETE https://co-life.herokuapp.com/api/v1/homes/:id`

Successfull HTTP response: `200 OK`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The id of the ad you want to delete

# Favorites

## Create

```shell
curl https://co-life.herokuapp.com/api/v1/favorites
  -X POST 
  -H "Content-Type: application/json" 
  -H "X-User-Email: example@testdomain.com" 
  -H "X-User-Token: <authentication_token>" 
  -d '{
    "favorite":{
      "home_id": "2"
    }
  }'
```

> The above command returns JSON structured like this:

```json
[
  {
    "user_id": 1,
    "home_id": 2
  }
]
```

Adds a home ad to the user's favorite list.

### HTTP Request

`POST https://co-life.herokuapp.com/api/v1/favorites`

Successfull HTTP response: `201 Created`

### Query Parameters

Parameter | Description
--------- | -----------
home_id | The id of the ad you want to add to your favorite list

## Index

```shell
curl https://co-life.herokuapp.com/api/v1/favorites
  -X GET
  -H "X-User-Email: example@testdomain.com"
  -H "X-User-Token: <authentication_token>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "user_id": 1,
    "home_id": 2
  },
  ...,
  {
    "user_id": 1,
    "home_id": 20
  }
]
```

Retrieves favorited home ads ids.

<aside class="notice">Users can only retrieve their own favorites. Admins can view everybody's favorites.</aside>

### HTTP Request

`GET https://co-life.herokuapp.com/api/v1/favorites`

Successfull HTTP response: `200 OK`

## Destroy

```shell
curl https://co-life.herokuapp.com/api/v1/favorites/1_20
  -X DELETE 
  -H "X-User-Email: example@testdomain.com" 
  -H "X-User-Token: <authentication_token>" 
```

> The above command returns JSON structured like this:

```json
[
  {
    "Ad removed from your favorites list!"
  }
]
```

Removes ad from the user's favorite list.

### HTTP Request

`DELETE https://co-life.herokuapp.com/api/v1/favorites/:user_home`

Successfull HTTP response: `200 OK`

### Query Parameters

Parameter | Description
--------- | -----------
user_home | User ID and home ID separated by an underline.
