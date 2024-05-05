---
title: Reference Endpoints
description: Instructions, endpoints and examples for the Reference resource group.
category: Developer Guide
---

# {{ $frontmatter.title }}

[[toc]]

The Reference resource group allows you to list or add a Reference to a given record. A Record may only have a single Reference, so ensure you check for an existing Reference on your Record before attempting to add one.

### Fetch Reference by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/references/{id}`
- Method: `GET`
- Params:
  - Allowed: `record id in endpoint url`
  - Required: `record id in endpoint url`

:::

Request:

```bash
--url API_URL/api/2.1/references/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `resource | error`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 8101,
  "message": "Single reference listing.",
  "data": {
    "id": 3644,
    "address1": "1234 Street Rd",
    "address2": null,
    "city": "City of Sustainability",
    "state": "CA",
    "postal": "98210",
    "country": "USA",
    "website": "www.example.com",
    "contact": "Lex Luthor",
    "title": "Evil Genius",
    "phone": "123-456-7890",
    "email": "lex@example.com",
    "created": "2018-04-17 03:54:21",
    "updated": "2018-04-17 03:54:21"
  }
}
```

### Filter Reference by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/references/{id}`
- Method: `PUT`
- Params:
  - Allowed:
    - `(array)filters`
  - Available Filters:
    - `(string)record`
    - `(string)preparer`
    - `(string)verifier`
  - Required:
    - `at least one available filter`
    - `record id in endpoint url`

:::

Request:

```bash
curl --request PUT \
  --url API_URL/api/2.1/references/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ 'filters': ['records','preparer','verifier'] }" \
```

Response returns: `resource | error`

```json{21-51}
{
  "http_status": 200,
  "http_message": "OK",
  "status": 8107,
  "message": "Filtered single reference listing.",
  "data": {
    "id": 3644,
    "address1": "1234 Street Rd",
    "address2": null,
    "city": "City of Sustainability",
    "state": "CA",
    "postal": "98210",
    "country": "USA",
    "website": "www.example.com",
    "contact": "Lex Luthor",
    "title": "Evil Genius",
    "phone": "123-456-7890",
    "email": "lex@example.com",
    "created": "2018-04-17 03:54:21",
    "updated": "2018-04-17 03:54:21",
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
    },
    "preparer": {
      "id": 2,
      "name": "HPD Collaborative",
      "archived": false,
      "created": "2015-11-07 02:13:28",
      "updated": "2015-11-07 02:13:28"
    },
    "verifier": {
      "id": 3,
      "name": "Verifier Company, LLC",
      "archived": false,
      "created": "2015-11-08 01:52:45",
      "updated": "2015-11-08 01:52:45"
    }
  }
}
```

### Add Reference Data to Record

A Record may not have more than one Reference, so adding a Reference to a Record where one already exists will return an error.

::: abstract requirements

- Endpoint: `/api/2.1/references/{id}`
- Method: `POST`
- Params:
  - Allowed:
    - `(string)address_1`
    - `(string)address_2`
    - `(string)city`
    - `(string)state`
    - `(string)postal`
    - `(string)country`
    - `(string)website`
    - `(string)contact`
    - `(string)title`
    - `(string)phone`
    - `(string)email`
    - `(int)prepared_by`
    - `(int)verified_by`
  - Required: `record id in endpoint url`

:::

Request:

```bash
curl --request POST \
  --url API_URL/api/2.1/references/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ address1: '1234 Street Rd',address2: '',city: 'City of Sustainability',state: 'CA',postal: '98210',country: 'USA',website: 'www.example.com',contact: 'Lex Luthor',title: 'Evil Genius',phone: '123-456-7890',email: 'lex@example.com',prepared_by: 2,verified_by: 3 }" \
```

Response returns: `resource | error`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 8102,
  "message": "Reference created successfully.",
  "data": {
    "id": 3644,
    "address1": "1234 Street Rd",
    "address2": null,
    "city": "City of Sustainability",
    "state": "CA",
    "postal": "98210",
    "country": "USA",
    "website": "www.example.com",
    "contact": "Lex Luthor",
    "title": "Evil Genius",
    "phone": "123-456-7890",
    "email": "lex@example.com",
    "created": "2018-04-17 03:54:21",
    "updated": "2018-04-17 03:54:21"
  }
}
```

## Special Notes

> [!tip]
> When creating a new Reference, use the [Companies](./companies) endpoint to create a list of available active companies for your `prepared_by` and `verified_by` variables.
>
> [Companies](./companies) produces an array to create a select menu for your UI.
