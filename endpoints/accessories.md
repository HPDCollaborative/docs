---
title: Accessories
description: Instructions, endpoints and examples for accessories.
---

[[toc]]

# Accessory Endpoints {.doc-heading}

The Accessory resource group contains endpoints for consuming and adding Accessories to a given Record. Responses are truncated for brevity.

### List Accessories by Record ID {.doc-heading}

::: abstract requirements

- Endpoint: `/api/2.1/accessories/{id}`
- Method: `GET`
- Params:
  - Allowed: `record id in endpoint url`
  - Required: `record id in endpoint url`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/accessories/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `collection | empty`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 5100,
  "message": "List of record accessories.",
  "data": [
    {
      "id": 1417,
      "name": "SUSTAIN 2300 ULTRA GREEN PLUS TILE ADHESIVE (VOC 0.00 G/L)",
      "website": "",
      "conditions": "Sustain Carpets recommended adhesive should be ...",
      "created": "2018-01-31 22:21:36",
      "updated": "2018-01-31 22:21:36"
    },
    ...
  ]
}
```

### Filter Accessories by Record ID {.doc-heading}

::: abstract requirements

- Endpoint: `/api/2.1/accessories/{id}`
- Method: `PUT`
- Params:
  - Allowed:
    - `(array)filters`
  - Available Filters:
    - `(string)records`
  - Required:
    - `at least one available filter`
    - `record id in endpoint url`

:::

Request:

```bash
curl --request PUT \
  --url API_URL/api/2.1/accessories/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ 'filters': ['records'] }"
```

Response returns: `collection | empty`

```json hl_lines="14"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 5105,
  "message": "Filtered list of record accessories.",
  "data": [
    {
      "id": 1417,
      "name": "SUSTAIN 2300 ULTRA GREEN PLUS TILE ADHESIVE (VOC 0.00 G/L)",
      "website": "",
      "conditions": "Sustain Carpets recommended adhesive should be ...",
      "created": "2018-01-31 22:21:36",
      "updated": "2018-01-31 22:21:36",
      "records": [
        {
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
        },
        ...
      ]
    },
    ...
  ]
}
```

### Fetch an Accessory by ID {.doc-heading}

::: abstract requirements

- Endpoint: `/api/2.1/accessories/{id}/show`
- Method: `GET`
- Params:
  - Allowed: `accessory id in endpoint url`
  - Required: `accessory id in endpoint url`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/accessories/{id}/show \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \

```

Response returns: `resource | 404`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 5101,
  "message": "Single accessory listing.",
  "data": {
    "id": 1417,
    "name": "SUSTAIN 2300 ULTRA GREEN PLUS TILE ADHESIVE (VOC 0.00 G/L)",
    "website": "",
    "conditions": "Sustain Carpets recommended adhesive should be ...",
    "created": "2018-01-31 22:21:36",
    "updated": "2018-01-31 22:21:36"
  }
}
```

### Filter an Accessory by ID {.doc-heading}

::: abstract requirements

- Endpoint: `/api/2.1/accessories/`
- Method: `PUT`
- Params:
  - Allowed:
    - `(array)filters`
  - Available Filters:
    - `(string)records`
  - Required:
    - `at least one available filter`
    - `accessory id in endpoint url`

:::

Request:

```bash
curl --request PUT \
  --url API_URL/api/2.1/accessories/{id}/show \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ 'filters': ['records'] }"
```

Response returns: `resource | 404`

```json hl_lines="13"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 5107,
  "message": "Filtered single accessory listing.",
  "data": {
    "id": 1417,
    "name": "SUSTAIN 2300 ULTRA GREEN PLUS TILE ADHESIVE (VOC 0.00 G/L)",
    "website": "",
    "conditions": "Sustain Carpets recommended adhesive should be ...",
    "created": "2018-01-31 22:21:36",
    "updated": "2018-01-31 22:21:36",
    "records": [
      {
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
      },
      ...
    ]
  }
}
```

### Add an Accessory to a Record {.doc-heading}

::: abstract requirements

- Endpoint: `/api/2.1/accessories/{id}`
- Method: `POST`
- Params:
  - Allowed:
    - `(string)name`
    - `(string)website`
    - `(string)conditions`
  - Required:
    - `(string)name`
    - `(string)conditions`
    - `record id in endpoint url`

:::

Request:

```bash
curl --request POST \
  --url API_URL/api/2.1/accessories/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ name: 'Test Accessory 1', website: 'http://example.com', conditions: 'Recommended for all installations.' }"
```

Response returns: `resource | validation errors`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 5102,
  "message": "Accessory created successfully.",
  "data": {
    "id": 1517,
    "name": "Test Accessory 1",
    "website": "http://example.com",
    "conditions": "Recommended for all installations.",
    "created": "2018-04-15 03:23:27",
    "updated": "2018-04-15 03:23:27"
  }
}
```
