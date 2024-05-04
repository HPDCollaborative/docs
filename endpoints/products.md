---
title: Product Endpoints
description: Instructions, endpoints and examples for products.
category: Developer Guide
---

[[toc]]

# {{ $frontmatter.title }}

A Product is the basis for building HPDs. In essence, an HPD is a [Record](records/) of what all your product contains, and you can have several HPD's for a single product.

Product endpoints can be used to list existing products, or create a new product.

### List All Products

> [!note] update
> The List All Products endpoint now allows you to pass in an optional company id number to list all the products belonging to a specific company that you are a member of.

::: abstract requirements

- Endpoint: `/api/2.1/products/{company?}`
- Method: `GET`
- Params:
  - Allowed: `company id in endpoint url (optional)`
  - Required: `NULL`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/products/{company?} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `resource collection | empty`

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
    ...
    ]
}
```

### Filter All Products

> [!note] update
> The Filter All Products endpoint now allows you to pass in an optional company id number to list all the products belonging to a specific company that you are a member of.

::: abstract requirements

- Endpoint `/api/2.1/products/{company?}`
- Method `PUT`
- Params:
  - Allowed:
    - `company id in endpoint url (optional)`
    - `(array)filters`
  - Available Filters:
    - `(string)company`
    - `(string)records`
  - Required: `at least one available filter`

:::

Request:

```bash
curl --request PUT \
  --url API_URL/api/2.1/products/{company?} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ 'filters': ['company','records'] }" \
```

Response returns: `collection | empty`

```json hl_lines="13 20"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 1105,
  "message": "Filtered list of products.",
  "data": [
    {
      "id": 1,
      "name": "Cushion Tile by Sustain Carpets",
      "archived": false,
      "created": "2015-11-08 01:23:47",
      "updated": "2015-11-08 01:23:47",
      "company": {
        "id": 2,
        "name": "HPD Collaborative",
        "archived": 0,
        "created": "2015-11-07 02:13:28",
        "updated": "2015-11-07 02:13:28"
      },
      "records": [
        {
          "id": 1,
          "format_id": 1,
          "stage_id": 3,
          "archived": false,
          "created": "2015-11-09 13:07:44",
          "updated": "2017-11-15 15:59:08",
          "published_filename": null,
          "published_at": null,
          "screened": "2017-06-08 00:00:00",
          "inventory_type": 5,
          "leed_calc": true,
          "leed_display": false,
          "no_accessory": false,
          "product": 1
        },
        ...
      ]
    },
    ...
  ]
}
```

### Fetch Product by ID

::: abstract requirements

- Endpoint: `/api/2.1/products/{id}`
- Method: `GET`
- Params:
  - Allowed: `product id in endpoint url`
  - Required: `product id in endpoint url`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/products/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `resource | 404`

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

### Filter Product by ID

::: abstract requirements

- Endpoint: `/api/2.1/products/{id}`
- Method: `PUT`
- Params:
  - Allowed:
    - `(array)filters`
  - Available Filters:
    - `(string)company`
    - `(string)records`
  - Required:
    - `at least one available filter`
    - `product id in endpoint url`

:::

Request:

```bash
curl --request PUT \
  --url API_URL/api/2.1/products/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ 'filters': ['company','records'] }" \
```

Response returns: `resource | 404`

```json hl_lines="12 19"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 1107,
  "message": "Filtered single product listing.",
  "data": {
    "id": 3710,
    "name": "Test Product",
    "archived": false,
    "created": "2018-03-27 09:02:35",
    "updated": "2018-03-27 09:02:35",
    "company": {
      "id": 2,
      "name": "HPD Collaborative",
      "archived": 0,
      "created": "2015-11-07 02:13:28",
      "updated": "2015-11-07 02:13:28"
    },
    "records": [
      {
        "id": 4910,
        "format_id": 4,
        "stage_id": 3,
        "archived": false,
        "created": "2018-03-27 09:07:01",
        "updated": "2018-03-27 09:07:01",
        "published_filename": null,
        "published_at": null,
        "screened": "2018-03-27 09:07:01",
        "inventory_type": 4,
        "leed_calc": false,
        "leed_display": false,
        "no_accessory": false,
        "product": 3710
      },
      ...
    ]
  }
}
```

### Create a New Product

::: abstract requirements

- Endpoint: `/api/2.1/products`
- Method: `POST`
- Params:
  - Allowed:
    - `(string)name`
    - `(integer)company_id`
  - Required:
    - `(string)name`

:::

Request:

```bash
curl --request POST \
  --url API_URL/api/2.1/products \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{ "name":"Your Product Name", "company_id": 12345 }'
```

Response returns: `resource | validation errors`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 1102,
  "message": "Product created successfully.",
  "data": {
    "id": 1234,
    "company": "Your Company",
    "name": "Your Product Name",
    "archived": null,
    "created": "2018-03-26 23:57:08",
    "updated": "2018-03-26 23:57:08"
  }
}
```
