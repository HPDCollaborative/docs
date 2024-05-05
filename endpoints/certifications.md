---
title: Certification Endpoints
description: Instructions, endpoints and examples for the Certifications resource group.
category: Developer Guide
---

# {{ $frontmatter.title }}

[[toc]]

## List Certifications by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/certifications/{id}`
- Method: `GET`
- Params:
  - Allowed: `record id in endpoint url`
  - Required: `record id in endpoint url`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/certifications/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `collection | null`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 7100,
  "message": "List of record certifications.",
  "data": [
    {
      "id": 2896,
      "owner_id": 2,
      "type": "VOC emissions",
      "other_type": "",
      "name": "CRI Green Label Plus - Carpet",
      "voc": null,
      "party": "Second Party",
      "issue": "2013-06-30 00:00:00",
      "expire": "2015-06-30 00:00:00",
      "lab": "Carpet & Rug Institute (CRI)",
      "facilities": "All Facilities.",
      "website": "",
      "notes": "",
      "pharos_id": null,
      "created": "2018-01-31 22:21:36",
      "updated": "2018-01-31 22:21:36"
    },
    ...
  ]
}
```

## List Certification by ID

::: abstract requirements

- Endpoint: `/api/2.1/certifications/{id}/show`
- Method: `GET`
- Params:
  - Allowed: `certification id in endpoint url`
  - Required: `certification id in endpoint url`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/certifications/{id}/show \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `resource | 404`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 7101,
  "message": "Single certification listing.",
  "data": {
    "id": 2897,
    "owner_id": 2,
    "type": "Multi-attribute",
    "other_type": "",
    "name": "NSF Sustainable Carpet Assessment ...",
    "voc": null,
    "party": "Second Party",
    "issue": "2014-12-18 00:00:00",
    "expire": "2015-12-18 00:00:00",
    "lab": "NSF International for CRI",
    "facilities": "All Facilities.",
    "website": "https://certificate-url.pdf",
    "notes": "",
    "pharos_id": null,
    "created": "2018-01-31 22:21:36",
    "updated": "2018-01-31 22:21:36"
  }
}
```

## Add a New Certification by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/certifications/{id}`
- Method: `POST`
- Params:
  - Allowed:
    - `(string)name`
    - `(string)voc`
    - `(string)type`
    - `(string)other_type`
    - `(string)party`
    - `(date)issue` _(format = Y-m-d)_
    - `(date)expire` _(format = Y-m-d > issue)_
    - `(string)lab`
    - `(text)facilities`
    - `(string)website`
    - `(text)notes`
  - Required:
    - `(string)name`
    - `(string)type`
    - `(string)other_type` _(required if type == Other)_
    - `(string)party`
    - `(date)issue` _(format = Y-m-d)_
    - `(string)lab`
    - `(text)facilities`

:::

Request:

```bash
curl --request POST \
  --url API_URL/api/2.1/certifications/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ name: 'CRI Green Label Plus - Carpet', type: 'VOC emissions', other_type: '', party: 'Second Party', issue: '2018-05-23', expire: '2019-05-30', lab: 'Carpet & Rug Institute (CRI)', facilities: 'All Facilities.', website: '', notes: '' }"
```

Response returns: `resource | validation errors`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 7102,
  "message": "Certification created successfully.",
  "data": {
    "id": 3044,
    "owner_id": 2,
    "type": "VOC emissions",
    "other_type": null,
    "name": "CRI Green Label Plus - Carpet",
    "voc": null,
    "party": "Second Party",
    "issue": "2018-05-23 00:00:00",
    "expire": "2019-05-30 00:00:00",
    "lab": "Carpet & Rug Institute (CRI)",
    "facilities": "All Facilities.",
    "website": null,
    "notes": null,
    "pharos_id": null,
    "created": "2018-05-23 06:49:57",
    "updated": "2018-05-23 06:49:57"
  }
}
```

## Selectable Options

> [!info]
> Use this endpoint to build radio buttons for your UI to select the allowed type and party for your certification

::: abstract requirements

- Endpoint: `/api/2.1/certifications/options`
- Method: `GET`
- Params: `none`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/certifications/options \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `array`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 7106,
  "message": "Certification selectable options.",
  "data": {
    "types": [
      "VOC content",
      "VOC emissions",
      "Biobased content",
      "Composite Wood",
      "Formaldehyde content",
      "Formaldehyde emissions",
      "LCA",
      "Management",
      "Material content migration",
      "Organic agriculture",
      "Recycled content",
      "Sustainable forestry",
      "Multi-attribute ",
      "Other"
    ],
    "parties": ["Self-declared", "Second Party", "Third Party"]
  }
}
```
