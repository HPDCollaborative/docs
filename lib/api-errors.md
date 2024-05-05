---
title: API Errors
description: API error message formats and examples.
category: Libraries & Errors
---

# {{ $frontmatter.title }}

[[toc]]

The HPDC API uses a very regimented and consistent messaging structure to return both errors and success messages for each and every request.

Your application, whether build in PHP, Javascript, ASP, Java or whatever language you've chosen, should rely on both HTTP status codes and messages to provide both developers and users with a consistent development and user experience.

## Message Format

All responses from the API are returned in JSON format for both simplicity and consistency.

All response will contain the following keys:

1. _(int)_ **`http_status`** - the HTTP status code of the response.
2. _(string)_ **`http_message`** - the RFC status text corresponding with the HTTP status code.
3. _(int)_ **`status`** - the HPDC internal message code.
4. _(string)_ **`message`** - the HPDC status text corresponding with the HPDC status code.
5. _(array)_ **`data`** - (optional) depending on whether errors exist.
6. _(array)_ **`error`** - (optional) only returned if errors exist in the request.

### Errors

If the response contains errors, you will receive an `error` array which will contain item 3 and 4 above, and the additional errors to be corrected.

If no errors exist, you will receive a `data` array with any data requested, and items 3 and 4 will be included in the main response.

Let's look at some examples.

### Examples

**This shows a status 200 response of product id 2:**

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 1101,
  "message": "Single product listing.",
  "data": {
    "id": 2,
    "company": "HPD Collaborative",
    "name": "Cushion Tile by Sustain Carpets",
    "archived": false,
    "created": "2015-11-10 22:20:17",
    "updated": "2015-11-10 22:20:17"
  }
}
```

**This shows an error response for a product that doesn't exist:**

> [!tip]
> Notice that the HPDC internal status and message are located inside the error array.

```json
{
  "http_status": 404,
  "http_message": "Not Found",
  "error": {
    "status": 1001,
    "message": "The requested product resource was not found."
  }
}
```

**This shows a 404 response for an endpoint that doesn't exist:**

```json
{
  "http_status": 404,
  "http_message": "Not Found",
  "error": {
    "status": 999,
    "message": "The requested endpoint was not found."
  }
}
```

**This example shows a POST response with validation errors:**

> [!tip]
> Notice the `invalid` array inside `error` that lists all the validation errors.

```json
{
  "http_status": 422,
  "http_message": "Unprocessable Entity",
  "error": {
    "status": 1000,
    "message": "Please correct any invalid fields.",
    "invalid": ["The name field is required."]
  }
}
```

**This shows a successful truncated request of a collection of products:**

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 1100,
  "message": "List of company products.",
  "data": [
    {
      "id": 1,
      "company": "HPD Collaborative",
      "name": "Cushion Tile by Sustain Carpets",
      "archived": false,
      "created": "2015-11-08 01:23:47",
      "updated": "2015-11-08 01:23:47"
    },
    {
      "id": 2,
      "company": "HPD Collaborative",
      "name": "Cushion Tile by Sustain Carpets",
      "archived": false,
      "created": "2015-11-10 22:20:17",
      "updated": "2015-11-10 22:20:17"
    },
    {
      "id": 24,
      "company": "HPD Collaborative",
      "name": "Copper",
      "archived": false,
      "created": "2015-11-18 17:46:25",
      "updated": "2015-11-18 17:46:25"
    },
    {
      "id": 30,
      "company": "HPD Collaborative",
      "name": "Test",
      "archived": false,
      "created": "2015-11-25 21:18:27",
      "updated": "2015-11-25 21:18:27"
    },
    {
      "id": 35,
      "company": "HPD Collaborative",
      "name": "SuperGreen Carpet ",
      "archived": false,
      "created": "2015-12-08 20:19:05",
      "updated": "2015-12-08 20:19:05"
    },
    ...
  ]
}
```

We've made it very simple to parse your responses by simply testing for response codes and the existence of the `error` array.

For a comprehensive list of all error and internal status codes, check out our [Response Code](./response-codes) list.
