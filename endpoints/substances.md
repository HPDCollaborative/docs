---
title: Substances
description: Substance creation on the API.
---

[[toc]]

# Substance Endpoints {.doc-heading}

## Add a Substance to a Material by ID {.doc-heading}

::: abstract requirements

- Endpoint: `/api/2.1/substances`
- Method: `POST`
- Params:
  - Allowed:
    - `(string)name`
    - `(string)cas`
    - `(integer)record_id`
    - `(integer)material_id`
    - `(string)gslt`
    - `(boolean)nocas` _(select only one of nocas, nocasorid, noid)_
    - `(boolean)nocasorid` _(select only one of nocas, nocasorid, noid)_
    - `(boolean)noid` _(select only one of nocas, nocasorid, noid)_
    - `(boolean)biobased`
    - `(integer)screened`
    - `(boolean)mask`
    - `(decimal)min`
    - `(decimal)max`
    - `(boolean)residual`
    - `(integer)nano` _(0 = No, 1 = Yes, 2 = Unknown)_
    - `(string)role`
    - `(string)recycle` _(select one - Both, PostC, PreC, None, UNK)_
    - `(text)notes`
  - Required:
    - `(string)name`
    - `(string)cas` _(if nocas nocasorid noid biobased are ALL false)_
    - `(integer)record_id`
    - `(integer)material_id`
    - `(string)gslt` _(if name and cas are null)_
    - `(decimal)min`
    - `(decimal)max` _(max > min && max <= 100)_
    - `(string)role`
    - `(integer)nano` _(0 = No, 1 = Yes, 2 = Unknown)_
    - `(string)recycle` _(select one - Both, PostC, PreC, None, UNK)_

:::

Request:

```bash
curl --request POST \
  --url API_URL/api/2.1/substances \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ record_id: 4925, material_id: 1207, name: 'PORTLAND CEMENT', cas: '65997-15-1', nocas: false, nocasorid: false, noid: false, biobased: '', screened: '', gslt: 'NoGS', mask: false, min: '100.00', max: '100.00', residual: '', nano: '0', role: 'Mixer', recycle: 'None', notes: '' }"
```

Response returns: `resource | validation errors`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 4100,
  "message": "Substance was added successfully.",
  "data": {
    "id": 36189,
    "owner_id": 2,
    "name": "PORTLAND CEMENT",
    "cas": "65997-15-1",
    "material_id": 1207,
    "pharos_id": 2007166,
    "gslt": "LT-P1",
    "nocas": false,
    "biobased": false,
    "created": "2018-05-23 08:26:51",
    "updated": "2018-05-23 08:26:53",
    "screened": 1,
    "nocasorid": false,
    "noid": false,
    "nohazard": false,
    "hazards": [
      {
        "id": 41,
        "name": "Potential Endocrine Disruptor",
        "sublist_id": 394,
        "list_name": "TEDX - Potential Endocrine Disruptors",
        "agency": "The Endocrine Disruption Exchange (TEDX)",
        "color": "orange",
        "endpoint": "ENDOCRINE",
        "endpoint_abbr": "END",
        "created": "2015-11-17 17:38:57",
        "updated": "2015-11-17 17:38:57"
      },
      {
        "id": 5,
        "name": "Carcinogen Group 3B - Evidence of carcinogenic ...",
        "sublist_id": 419,
        "list_name": "MAK",
        "agency": "MAK Commission of Germany (Deutsche Forschungsgemeinschaft)",
        "color": "orange",
        "endpoint": "CANCER",
        "endpoint_abbr": "CAN",
        "created": "2015-11-17 17:20:05",
        "updated": "2015-11-17 17:20:05"
      }
    ]
  }
}
```
