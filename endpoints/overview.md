---
title: API Overview
description: Overview and discussion of resource methods and basic example definitions.
---

[[toc]]

# API Overview {.doc-heading}

The purpose of this document is to provide developers with endpoints and required/allowed parameters to consume the HPDC API.

Prior to attempting to connect with the API, ensure you've read through the [OAuth2 Authentication](libraries/) requirements, and have a working implementation for your application. Details for Authentication can be found on the [Libraries page.](libraries/)

Examples below represent only successful requests that return an HTTP status code of 200, for information on message formats and error codes, see the [API Errors](api-errors/) or [Response Codes](response-codes/) pages.

## Endpoints {.doc-heading}

In our endpoint examples we'll show only basic CURL examples.

::: note
If you're using an HTTP library for your application such as [Guzzle](https://github.com/guzzle/guzzle) for PHP apps, or [Axios](https://github.com/axios/axios) for Node apps, you'll need to consult the package documentation for specific instructions on making successful HTTP requests.
:::

## Resource Methods {.doc-heading}

At present, the HPDC API accepts only the following resource methods:

1. **GET**
2. **PUT**
3. **POST**

The **DELETE** and **PATCH** methods are not accepted and will return **405 Method Not Allowed** exceptions. If you need to delete or edit products, records, etc., please log into your Builder account directly and edit or delete these items there.

**PUT** methods are used only for sending optional parameters in order to vary a given response. For instance if you wanted to request a base HPD Record by it's ID, you would send a **GET** request. If you wanted to request an advanced HPD Record by it's ID, and include all it's Materials and Accessories, this would be a **PUT** request.

::: warning
Once again to be clear, editing and deleted is **not supported** through the API at this time.
:::

## Examples {.doc-heading}

::: note
Endpoint code examples assume that you've stored both the root api url, and your OAuth token into a session, local storage, or another storage mechanism of your choosing so that they can be easily referenced via variable. For the purposes of our examples we will use the placeholders `API_URL` and `TOKEN` to hold the place of those variables.
:::

::: danger correct url
Ensure you're using the appropriate `API_URL` for your OAuth Client, development and production Clients and URLS are **NOT** interchangeable.
:::

An example request might look something similar to this:

```bash
curl --request GET \
  --url API_URL/api/2.1/me \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

This request would return a response showing your personal account info:

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 9000,
  "message": "Viewing my user info.",
  "data": {
    "name": "Your Name",
    "email": "youremail@example.com",
    "company": "Your Company",
    "joined": "2017-12-13 19:43:08",
    "updated": "2018-03-14 00:00:22"
  }
}
```
