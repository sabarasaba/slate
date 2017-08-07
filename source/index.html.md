---
title: Reminders API

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Reminders API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.reminders.sh/"
  -H "token: {{your_token}}"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `{{your_token}}` with your API key.

Reminders uses API keys to allow access to the API. You can register yourself for a new Reminders API key at our [developer portal](http://example.com/developers).

Reminders expects for the API key to be included in all API requests to the server in a header that looks like the following:

`token: {{your_token}}`

# Reminders

## Get All Reminders

```shell
curl "https://api.reminders.com/api/v1/reminders"
  -H "token: {{your_token}}"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 1,
      "user": "5978e2189950cbdaa2371710",
      "due": "2017-08-02T21:18:00.000Z",
      "timezone": "Europe/Amsterdam",
      "active": true,
      "email_to": null,
      "email_text": null,
      "email_html": null,
      "email_subject": null,
      "email_from": null,
      "sms_to": "+31615911049",
      "sms_body": "rico papi",
      "created_at": "2017-08-06T13:51:37.872Z",
      "updated_at": "2017-08-06T13:51:52.797Z"
    }
  ],
  "meta": {
    "sort": "id desc",
    "offset": 0,
    "limit": 20
  },
  "jsonapi": {
    "version": "1.0"
  }
}
```

This endpoint retrieves all of your reminders.

### HTTP Request

`GET https://api.reminders.com/api/v1/reminders`

### Query Parameters

Parameter | Default | Type | Required | Description
--------- | ------- | ----------- | ----------- | -----------
active | undefined | Boolean | No | If set to true it will return all active reminders, false all inactive reminders. Not set means all reminders.
offset | 0 | Integer | No | Sets the offset for the returned results
limit | 20 | Integer | No | Limits the amount of results returned.
sort | 'id desc' | String | No | Specifies the sort method for the retrieved collection.

## Get a Specific Reminder

```shell
curl "https://api.reminders.com/api/v1/reminders/<ID>"
  -H "token: {{your_token}}"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 13,
    "user": "5978e2189950cbdaa2371710",
    "due": "2017-08-01T19:40:00.000Z",
    "timezone": "Europe/Amsterdam",
    "active": false,
    "email": "asd@asd.com",
    "email_body": "hola papito lindoooo",
    "email_subject": null,
    "email_from": null,
    "created_at": "2017-08-01T19:39:02.953Z"
  },
  "jsonapi": {
    "version": "1.0"
  }
}
```

This endpoint retrieves a specific reminder.

### HTTP Request

`GET https://api.reminders.com/api/v1/reminders/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Reminder to retrieve

## Create a Reminder

```shell
curl "https://api.reminders.com/api/v1/reminders"
  -X POST
  -H "token: {{your_token}}"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "status": "ok"
  },
  "jsonapi": {
    "version": "1.0"
  }
}
```

This endpoint allows you to create a new Reminder.

### HTTP Request

`POST https://api.reminders.com/api/v1/reminders`

### Query Parameters

Parameter | Default | Type | Required | Description
--------- | ------- | -----------| -----------| -----------
due | undefined | Date | Yes | The date the reminder is due for.
timezone | Accounts default timezone | String | No | Overrides accounts default timezone for this specific reminder.
force | false | Boolean | No | Skips validation of due date to check if it happened in the past.
email_to | undefined | String | No | Skips validation of due date to check if it happened in the past.
email_from | undefined | String | No | Skips validation of due date to check if it happened in the past.
email_subject | undefined | String | No | Skips validation of due date to check if it happened in the past.
email_text | undefined | String | No | Skips validation of due date to check if it happened in the past.
email_html | undefined | String | No | Skips validation of due date to check if it happened in the past.
sms_to | undefined | String | No | Skips validation of due date to check if it happened in the past.
sms_body | undefined | String | No | Skips validation of due date to check if it happened in the past.


<aside class="warning">
  You are required to either create a reminder for an email, or sms or both. if you include `email_to` but dont include on of the other `email_*` arguments the API will give you an error. Same for `sms_*` fields.
</aside>

## Update a Reminder

```shell
curl "https://api.reminders.com/api/v1/reminders/2"
  -X PUT
  -H "token: {{your_token}}"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "status": "ok"
  },
  "jsonapi": {
    "version": "1.0"
  }
}
```

This endpoint Updates a specific Reminder.

### HTTP Request

`PUT https://api.reminders.com/api/v1/reminders/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Reminder to Update

### Query Parameters

Parameter | Default | Type | Required | Description
--------- | ------- | -----------| -----------| -----------
due | undefined | Date | No | The date the reminder is due for.
timezone | Accounts default timezone | String | No | Overrides accounts default timezone for this specific reminder.
force | false | Boolean | No | Skips validation of due date to check if it happened in the past.
email_to | undefined | String | No | Skips validation of due date to check if it happened in the past.
email_from | undefined | String | No | Skips validation of due date to check if it happened in the past.
email_subject | undefined | String | No | Skips validation of due date to check if it happened in the past.
email_text | undefined | String | No | Skips validation of due date to check if it happened in the past.
email_html | undefined | String | No | Skips validation of due date to check if it happened in the past.
sms_to | undefined | String | No | Skips validation of due date to check if it happened in the past.
sms_body | undefined | String | No | Skips validation of due date to check if it happened in the past.

## Delete a Specific Reminder

```shell
curl "https://api.reminders.com/api/v1/reminders/2"
  -X DELETE
  -H "token: {{your_token}}"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "status": "ok"
  },
  "jsonapi": {
    "version": "1.0"
  }
}
```

This endpoint retrieves a specific Reminder.

### HTTP Request

`DELETE https://api.reminders.com/api/v1/reminders/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Reminder to delete

