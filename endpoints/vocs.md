---
title: VOC Endpoints
description: Instructions, endpoints and examples for the VOC resource group.
category: Developer Guide
---

# {{ $frontmatter.title }}

[[toc]]

The VOC resource group allows you to list or add a VOC to a given record. A Record may only have a single VOC, so ensure you check for an existing VOC on your Record before attempting to add one.

### Fetch VOC by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/vocs/{id}`
- Method: `GET`
- Params:
  - Allowed: `record id in endpoint url`
  - Required: `record id in endpoint url`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/vocs/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `resource | error`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 6101,
  "message": "Record VOC listing.",
  "data": {
    "id": 654,
    "voccontent": true,
    "material": "3",
    "regulatory": "6.7",
    "exempt": false,
    "ultra": 3,
    "created": "2018-04-20 14:57:54",
    "updated": "2018-04-20 14:57:54",
    "record": 4632
}
```

### Filter VOC by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/vocs/{id}`
- Method: `PUT`
- Params:
  - Allowed:
    - `(array)filters`
  - Allowed Filters
    - `(string)record`
  - Required:
    - `at least one available filter`
    - `record id in endpoint url`

:::

Request:

```bash
curl --request PUT \
  --url API_URL/api/2.1/vocs/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ 'filters': ['records'] }"
```

Response returns: `response | error`

```json hl_lines="15"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 6107,
  "message": "Filtered single VOC listing.",
  "data": {
    "id": 654,
    "voccontent": true,
    "material": "3",
    "regulatory": "6.7",
    "exempt": false,
    "ultra": 3,
    "created": "2018-04-20 14:57:54",
    "updated": "2018-04-20 14:57:54",
    "record": {
      "id": 4632,
      "format_id": 4,
      "stage_id": 3,
      "archived": false,
      "created": "2018-01-31 22:21:35",
      "updated": "2018-01-31 22:21:35",
      "published_filename": null,
      "published_at": null,
      "screened": "2017-03-24 00:00:00",
      "inventory_type": 4,
      "leed_calc": false,
      "leed_display": false,
      "no_accessory": false,
      "product": 2
    }
  }
}
```

### Add VOC to Record

::: abstract requirements

- Endpoint: `/api/2.1/vocs/{id}`
- Method: `POST`
- Params:
  - Allowed:
    - `(boolean)voccontent`
    - `(string)material`
    - `(string)regulatory`
    - `(boolean)exempt`
    - `(integer)ultra`
  - Required:
    - `record id in endpoint url`
    - `if voccontent is true, all fields are required`

:::

Request:

```bash
curl --request POST \
  --url API_URL/api/2.1/references/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ voccontent: true, material: '3', regulatory: '67', exempt: false, ultra: 3 }" \
```

Response returns: `response | errors`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 6101,
  "message": "Record VOC listing.",
  "data": {
    "id": 654,
    "voccontent": true,
    "material": "3",
    "regulatory": "6.7",
    "exempt": false,
    "ultra": 3,
    "created": "2018-04-20 14:57:54",
    "updated": "2018-04-20 14:57:54",
    "record": 4632
  }
}
```
