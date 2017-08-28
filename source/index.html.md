---
title: Reminders.company API

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='/signup'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Reminders.company API! You can use our API to access and manage all your reminders and set different types of notifications for them.

We have language bindings in Shell and Javascript.! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.reminders.company/v1"
  -H "token: {{your_token}}"
```

```javascript
const request = require('request-promise')

await request({
  uri: 'https://api.reminders.company/v1',
  headers: {
    token: process.env.REMINDERS_API
  }
})
```

> Make sure to replace `{{your_token}}` with your API key.

Reminders uses API keys to allow access to the API. You can register yourself for a new Reminders API key at our [developer portal](/signup).

Reminders expects for the API key to be included in all API requests to the server in a header that looks like the following:

`token: {{your_token}}`

# Reminders

## Get All Reminders

```shell
curl "https://api.reminders.company/v1/reminders"
  -H "token: {{your_token}}"
```

```javascript
const request = require('request-promise')

const reminders = await request({
  uri: 'https://api.reminders.company/v1/reminders',
  headers: {
    token: process.env.REMINDERS_API
  }
})
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
      "email_body": null,
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

`GET https://api.reminders.company/v1/reminders`

### Query Parameters

Parameter | Default | Type | Required | Description
--------- | ------- | ----------- | ----------- | -----------
active | undefined | Boolean | No | If set to true it will return all active reminders, false all inactive reminders. Not set means all reminders.
offset | 0 | Integer | No | Sets the offset for the returned results
limit | 20 | Integer | No | Limits the amount of results returned.
sort | 'id desc' | String | No | Specifies the sort method for the retrieved collection.

## Get a Specific Reminder

```shell
curl "https://api.reminders.company/v1/reminders/<ID>"
  -H "token: {{your_token}}"
```

```javascript
const request = require('request-promise')

const reminder = await request({
  uri: 'https://api.reminders.company/v1/reminders/<ID>',
  headers: {
    token: process.env.REMINDERS_API
  }
})
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

`GET https://api.reminders.company/v1/reminders/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Reminder to retrieve

## Create a Reminder

```shell
curl "https://api.reminders.company/v1/reminders"
  -X POST
  -H "token: {{your_token}}"
  -d '{"due":"2017-08-02 23:18","sms_to":"+3159999999", "sms_body": "hello world"}'
```

```javascript
const request = require('request-promise')

await request({
  uri: 'https://api.reminders.company/v1/reminders',
  method: 'POST',
  headers: {
    token: process.env.REMINDERS_API
  },
  body: {
    due: '2017-08-02 23:18',
    sms_to: '+3159999999',
    sms_body: 'hello world'
  }
})
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

This endpoint allows you to create a new Reminder. Timezone format follows the naming convention of [moment.timezone](https://momentjs.com/timezone/).

### HTTP Request

`POST https://api.reminders.company/v1/reminders`

### Query Parameters

Parameter | Default | Type | Required | Description
--------- | ------- | -----------| -----------| -----------
due | undefined | Date | Yes | The date the reminder is due for.
timezone | Accounts default timezone | String | No | Overrides accounts default timezone for this specific reminder.
force | false | Boolean | No | Skips validation of due date to check if it happened in the past.
email_to | undefined | String | No | Skips validation of due date to check if it happened in the past.
email_from | undefined | String | No | Skips validation of due date to check if it happened in the past.
email_subject | undefined | String | No | Skips validation of due date to check if it happened in the past.
email_body | undefined | String | No | Skips validation of due date to check if it happened in the past.
sms_to | undefined | String | No | Skips validation of due date to check if it happened in the past.
sms_body | undefined | String | No | Skips validation of due date to check if it happened in the past.


<aside class="warning">
  You are required to either create a reminder for an email, or sms or both. if you include `email_to` but dont include on of the other `email_*` arguments the API will give you an error. Same for `sms_*` fields.
</aside>

## Update a Reminder

```shell
curl "https://api.reminders.company/v1/reminders/<ID>"
  -X PUT
  -H "token: {{your_token}}"
  -d '{"sms_body": "hello world !"}'
```

```javascript
const request = require('request-promise')

await request({
  uri: 'https://api.reminders.company/v1/reminders/<ID>',
  method: 'PUT',
  headers: {
    token: process.env.REMINDERS_API
  },
  body: {
    sms_body: 'hello world !'
  }
})
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

`PUT https://api.reminders.company/v1/reminders/<ID>`

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
email_body | undefined | String | No | Skips validation of due date to check if it happened in the past.
sms_to | undefined | String | No | Skips validation of due date to check if it happened in the past.
sms_body | undefined | String | No | Skips validation of due date to check if it happened in the past.

## Delete a Specific Reminder

```shell
curl "https://api.reminders.company/v1/reminders/<ID>"
  -X DELETE
  -H "token: {{your_token}}"
```

```javascript
const request = require('request-promise')

await request({
  uri: 'https://api.reminders.company/v1/reminders/<ID>',
  method: 'DELETE',
  headers: {
    token: process.env.REMINDERS_API
  }
})
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

`DELETE https://api.reminders.company/v1/reminders/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Reminder to delete

# Utils

## Get account usage

```shell
curl "https://api.reminders.company/v1/usage"
  -H "token: {{your_token}}"
```

```javascript
const request = require('request-promise')

const reminders = await request({
  uri: 'https://api.reminders.company/v1/usage',
  headers: {
    token: process.env.REMINDERS_API
  }
})
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "plan": {
      "emails": 200,
      "sms": 0,
      "webhook": false
    },
    "usage": {
      "emails": 1,
      "sms": 0
    }
  },
  "jsonapi": {
    "version": "1.0"
  }
}
```

This endpoint retrieves your current plan and usage of your account for the current period of time. A period of time starts on the first of each month and finishes the next first of the month.

### HTTP Request

`GET https://api.reminders.company/v1/usage`

