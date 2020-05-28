---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Users

## Sign Up

```shell
curl http://127.0.0.1:3000/users
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

### HTTP Request

`POST http://127.0.0.1:3000/users`

### Query Parameters

Parameter | Description
--------- | -----------
name | The account's user name
email | The account's email
password | The account's password
password_confirmation | Password confirmation

## Update

```shell
curl http://127.0.0.1:3000/users/1
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

`POST http://127.0.0.1:3000/users/:id`

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
curl http://127.0.0.1:3000/users/1
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

`GET http://127.0.0.1:3000/users/:id`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The id of the user you want to check

## Index

```shell
curl http://127.0.0.1:3000/users
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

`GET http://127.0.0.1:3000/users`

## Destroy

```shell
curl http://127.0.0.1:3000/users/1
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

<aside class="notice">Common users can only delete their own accounts. Admins can delete any common accounts.</aside>

### HTTP Request

`DELETE http://127.0.0.1:3000/users/:id`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The id of the user you want to delete

# Homes

## Create

```shell
curl http://127.0.0.1:3000/api/v1/homes 
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

`POST http://127.0.0.1:3000/api/v1/homes`

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
curl http://127.0.0.1:3000/api/v1/homes/1 
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

`GET http://127.0.0.1:3000/api/v1/homes/:id`

### Query Parameters

Parameter | Description
--------- | -----------
ID | The id of the ad you want to check

## Index

```shell
curl http://127.0.0.1:3000/api/v1/homes 
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

`GET http://127.0.0.1:3000/api/v1/homes`

## Update

```shell
curl http://127.0.0.1:3000/api/v1/homes/1
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

`PUT http://127.0.0.1:3000/api/v1/homes/:id`

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
curl http://127.0.0.1:3000/api/v1/homes/1
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

`DELETE http://127.0.0.1:3000/api/v1/homes/:id`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The id of the ad you want to delete

# Favorites

## Create

```shell
curl http://127.0.0.1:3000/api/v1/favorites
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

Adds a home add to the user's favorite list.

### HTTP Request

`POST http://127.0.0.1:3000/api/v1/homes`

### Query Parameters

Parameter | Description
--------- | -----------
home_id | The id of the ad you want to add to your favorite list

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

