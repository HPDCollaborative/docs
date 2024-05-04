---
title: Material Endpoints
description: Instructions, endpoints and examples for records.
category: Developer Guide
---

[[toc]]

# {{ $frontmatter.title }}

The Materials resource contains an extra endpoint to assist in the creation of UI's in your application. Make sure you check this out and utilize it when adding Materials to a record.

### List Materials by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/materials/{id}`
- Method: `GET`
- Params:
  - Allowed: `record id in endpoint url`
  - Required: `record id in endpoint url`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/materials/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `collection | empty`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 3100,
  "message": "List of record materials.",
  "data": [
    {
      "id": 30,
      "owner_id": 2,
      "name": "FACE YARN",
      "manufacturer": "HPD Collaborative",
      "created": "2015-11-17 14:44:42",
      "updated": "2015-11-17 14:44:42",
      "alternate": 0,
      "reportable": 0,
      "hpd_url": "",
      "threshold": 4,
      "residuals": 0,
      "residual_notes": null
    },
    ...
  ]
}
```

### Filter Materials by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/materials/{id}`
- Method: `PUT`
- Params:
  - Allowed:
    - `(array)filters`
  - Available Filters:
    - `(string)records`
    - `(string)substances`
  - Required:
    - `at least one available filter`
    - `record id in endpoint url`

:::

Request:

```bash
curl --request PUT \
  --url API_URL/api/2.1/materials/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ 'filters': ['records','substances'] }"
```

Response returns: `collection | empty`

```json hl_lines="20 39"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 3105,
  "message": "Filtered list of record materials.",
  "data": [
    {
      "id": 30,
      "owner_id": 2,
      "name": "FACE YARN",
      "manufacturer": "HPD Collaborative",
      "created": "2015-11-17 14:44:42",
      "updated": "2015-11-17 14:44:42",
      "alternate": 0,
      "reportable": 0,
      "hpd_url": "",
      "threshold": 4,
      "residuals": 0,
      "residual_notes": null,
      "records": [
        {
          "id": 3,
          "format_id": 1,
          "stage_id": 3,
          "archived": false,
          "created": "2015-11-11 12:19:26",
          "updated": "2017-08-01 02:37:12",
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
      ],
      "substances": [
        {
          "id": 145,
          "owner_id": 3,
          "name": "NYLON 6,6",
          "cas": "32131-17-2",
          "material_id": null,
          "pharos_id": null,
          "gslt": "LT-UNK",
          "nocas": 0,
          "biobased": 0,
          "created": "2015-11-17 14:47:43",
          "updated": "2015-11-17 14:47:43",
          "screened": 0,
          "nocasorid": 0,
          "noid": 0,
          "nohazard": 0,
          "mask": 0,
          "min": "52.2000",
          "max": "0.0000",
          "residual": 0,
          "recycle": "PostC",
          "nano": 0,
          "role": "Face Fiber",
          "notes": "No warnings found on HPD Priority lists"
        },
        ...
      ]
    },
    ...
  ]
}
```

### Fetch a Material by ID

::: abstract requirements

- Endpoint: `/api/2.1/materials/{id}/show`
- Method: `GET`
- Params:
  - Allowed: `material id in endpoint url`
  - Required: `material id in endpoint url`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/materials/{id}/show \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `resource | 404`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 3101,
  "message": "Single material listing.",
  "data": {
    "id": 1207,
    "owner_id": 2,
    "name": "Portland Cement",
    "manufacturer": "HPD Collaborative",
    "created": "2016-08-16 17:00:14",
    "updated": "2016-08-16 17:00:14"
  }
}
```

### Filter a Material by ID

::: abstract requirements

- Endpoint: `/api/2.1/materials/{record-id}/{material-id}/show`
- Method: `PUT`
- Params:
  - Allowed:
    - `(array)filters`
  - Available Filters:
    - `(string)records`
    - `(string)substances`
  - Required:
    - `at least one available filter`
    - `record id in endpoint url`
    - `material id in endpoint url`

:::

Request:

```bash
curl --request PUT \
  --url API_URL/api/2.1/materials/{record-id}/{material-id}/show \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ 'filters': ['records','substances'] }"
```

Response returns: `resource | 404`

```json hl_lines="19 38"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 3107,
  "message": "Filtered single material listing.",
  "data": {
    "id": 1207,
    "owner_id": 2,
    "name": "Portland Cement",
    "manufacturer": "HPD Collaborative",
    "created": "2016-08-16 17:00:14",
    "updated": "2016-08-16 17:00:14",
    "alternate": 0,
    "reportable": 0,
    "hpd_url": null,
    "threshold": 4,
    "residuals": 0,
    "residual_notes": null,
    "records": [
      {
        "id": 835,
        "format_id": 1,
        "stage_id": 3,
        "archived": false,
        "created": "2016-08-16 15:44:58",
        "updated": "2017-08-01 02:37:13",
        "published_filename": "publish_2_Ready_Mixed_Concrete_1475637738.pdf",
        "published_at": "2016-10-05 03:22:18",
        "screened": "2016-10-05 00:00:00",
        "inventory_type": 4,
        "leed_calc": false,
        "leed_display": false,
        "no_accessory": false,
        "product": 829
      },
      ...
    ],
    "substances": [
      {
        "id": 6977,
        "owner_id": 835,
        "name": "PORTLAND CEMENT",
        "cas": "65997-15-1",
        "material_id": 65997,
        "pharos_id": 2007166,
        "gslt": "LT-P1",
        "nocas": 0,
        "biobased": 0,
        "created": "2016-08-16 16:01:06",
        "updated": "2017-03-17 15:26:19",
        "screened": 0,
        "nocasorid": 0,
        "noid": 0,
        "nohazard": 0,
        "mask": 0,
        "min": "100.0000",
        "max": "100.0000",
        "residual": 0,
        "recycle": "None",
        "nano": 0,
        "role": "Mixer",
        "notes": ""
      }
    ]
  }
}
```

### Add a Material to a Record

::: abstract requirements

- Endpoint: `/api/2.1/materials/{id}`
- Method: `POST`
- Params:
  - Allowed:
    - `(string)name`
    - `(decimal)min`
    - `(decimal)max`
    - `(bool)mask`
    - `(bool)alternate`
    - `(bool)unreportable`
    - `(string)hdp_url`
    - `(int)threshold`
    - `(int)residuals` _(0: Not Considered, 1: Considered, 2: Partially Considered)_
    - `(text)notes`
    - `(text)residual_notes`
  - Required:
    - `(string)name`
    - `(decimal)min`
    - `record id in endpoint url`

:::

Request:

```bash
curl --request POST \
  --url API_URL/api/2.1/materials/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ name: 'Test Material', mask: 0, min: 35, max: 55, alternate: 1, unreportable: 1, hpd_url: 'http://example.com', threshold: 3, residuals: 1, residual_notes: 'Test residual notes for this testing material.', notes: 'Test notes' }"
```

Response returns: `resource | validation errors`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 3102,
  "message": "Material created successfully.",
  "data": {
    "id": 6965,
    "owner_id": 2,
    "name": "Test Material",
    "manufacturer": "HPD Collaborative",
    "created": "2018-04-10 09:07:28",
    "updated": "2018-04-10 09:07:28",
    "alternate": 0,
    "reportable": 0,
    "hpd_url": null,
    "threshold": 4,
    "residuals": 0,
    "residual_notes": null
  }
}
```
