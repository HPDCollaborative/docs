---
title: Note Endpoints
description: Instructions, endpoints and examples for the Note model.
category: Developer Guide
---

[[toc]]

# {{ $frontmatter.title }}

The Note resource group allows you to list or add Note data to a given record. A Record may only have a single Note, so ensure you check for an existing Note on your Record before attempting to add data to one.

### Fetch Note by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/notes/{id}`
- Method: `GET`
- Params:
  - Allowed: `record id in endpoint url`
  - Required: `record id in endpoint url`

:::

Request:

```bash
--url API_URL/api/2.1/notes/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `resource | 404`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 4501,
  "message": "Single note listing.",
  "data": {
    "id": 5604,
    "general": "This product has undergone the Cradle to ...",
    "created": "2018-09-30 22:52:07",
    "updated": "2018-09-30 22:52:07",
    "record": 6023
  }
}
```

### Filter Note by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/notes/{id}`
- Method: `PUT`
- Params:
  - Allowed:
    - `(array)filters`:
  - Available Filters:
    - `(string)record`
  - Required:
    - `at least one available filter`
    - `record id in endpoint url`

:::

Request:

```bash
curl --request PUT \
  --url API_URL/api/2.1/notes/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ 'filters': ['records'] }" \
```

Response returns: `resource | error`

```json hl_lines="11"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 4507,
  "message": "Filtered single note listing.",
  "data": {
    "id": 5604,
    "general": "This product has undergone the Cradle to ...",
    "created": "2018-09-30 22:52:07",
    "updated": "2018-09-30 22:52:07",
    "record": {
      "id": 6023,
      "format_id": 5,
      "stage_id": 3,
      "archived": false,
      "created": "2018-07-10 21:44:03",
      "updated": "2019-07-10 19:39:17",
      "published_filename": "publish_2_Cushion_Tile_by_Sustain_Carpets.pdf",
      "published_at": null,
      "screened": "2019-07-10 19:39:17",
      "inventory_type": 4,
      "leed_calc": true,
      "leed_display": true,
      "no_accessory": false,
      "product": 1
    }
  }
}
```

### Add Data to Note by Record ID

Adding data to a Note serves as an update to the existing empty Note created during the record creation process. No new Note is created.

::: abstract requirements

- Endpoint: `/api/2.1/notes/{id}`
- Method: `POST`
- Params:
  - Allowed:
    - `(text)general`
  - Required:
    - `record id in endpoint url`

:::

Request:

```bash
curl --request POST \
  --url API_URL/api/2.1/references/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{ "general": "This product has undergone the Cradle to ..." }' \
```

Response returns: `resource | error`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 4502,
  "message": "Note created successfully.",
  "data": {
    "id": 5604,
    "general": "This product has undergone the Cradle to ...",
    "created": "2018-09-30 22:52:07",
    "updated": "2019-08-09 10:52:35",
    "record": 6023
  }
}
```
