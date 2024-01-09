---
title: Record Endpoints
description: Instructions, endpoints and examples for records.
---

[[toc]]

# Record Endpoints {.doc-heading}

Records are arguably the most important aspect of building an HPD. In fact a Record **IS** an HPD. All the other parts of an HPD are tied to a given Record such as [Materials,](materials/) [Accessories,](accessories/) [References,](references/) [VOC's,](vocs/) [Certifications](certifications/) etc. When you publish an HPD to the [HPD Public Repository,](https://www.hpd-collaborative.org/hpd-public-repository/) in fact you are publishing a **_Record_**, and it's associated properties.

There are several different ways to interact with Records via the API.

### List Records by Product ID {.doc-heading}

::: abstract requirements

- Endpoint: `/api/2.1/records/{id}`
- Method: `GET`
- Params:
  - Allowed: `product id in endpoint url`
  - Required: `product id in endpoint url`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/records/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `resource collection | empty`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 2100,
  "message": "List of product records.",
  "data": [
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
  ]
}
```

### Filter Records by Product ID {.doc-heading}

::: abstract requirements

- Endpoint: `/api/2.1/records/{id}`
- Method: `PUT`
- Params:
  - Allowed:
    - `(array)filters`
  - Available filters:
    - `(string)product` _(always includes company)_
    - `(string)owner`
    - `(string)format`
    - `(string)detail`
    - `(string)materials`
    - `(string)note`
    - `(string)substances` _(requires materials)_
    - `(string)reference`
    - `(string)vocs`
    - `(string)accessories`
    - `(string)certifications`
    - `(string)summary`
  - Required:
    - `At least one allowed filter`
    - `product id in endpoint url`

:::

Request:

```bash
curl --request PUT \
  --url API_URL/api/2.1/records/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ 'filters': ['product','owner','format','detail','materials','substances','reference','vocs','accessories','certifications','summary'] }" \
```

Response returns: `resource collection | error`

```json hl_lines="21 27 35 42 52 64 82 113 129 140 151 172"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 2105,
  "message": "Filtered list of product records.",
  "data": [
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
      "product": {
        "id": 2,
        "name": "Cushion Tile by Sustain Carpets",
        "archived": false,
        "created": "2015-11-10 22:20:17",
        "updated": "2015-11-10 22:20:17",
        "company": {
          "id": 2,
          "name": "HPD Collaborative",
          "archived": 0,
          "created": "2015-11-07 02:13:28",
          "updated": "2015-11-07 02:13:28"
        }
      },
      "owner": {
        "id": 2,
        "name": "HPD Collaborative",
        "archived": 0,
        "created": "2015-11-07 02:13:28",
        "updated": "2015-11-07 02:13:28"
      },
      "format": {
        "id": 4,
        "name": "Health Product Declaration",
        "version": "2.1",
        "abbreviation": "HPD",
        "publishable": 1,
        "archived": 0,
        "created": "2017-08-01 02:37:07",
        "updated": "2017-08-01 02:37:07"
      },
      "detail": {
        "id": 4306,
        "classification": "09 68 13 Tile Carpeting ",
        "description": "This HPD covers all products on Sustain Carpet’s Sustain® Cushion Tile. Products construction includes Nylon 6,6 face fiber, thermoplastic laminate, polyurethane cushion and Sustain® scrim.",
        "threshold_type": "Material",
        "inventory_notes": "This product has undergone the Cradle to Cradle Certification™ material health evaluation and has achieved Silver level certification. The assessment is\r\nconducted by an accredited assessor with expertise in toxicology and chemistry. Companies pursuing certification commit to phasing out problematic\r\ningredients that have been identified. The material health score indicates how much progress has been made in optimizing the product. Sustain’s standard\r\nbroadloom, High PerformancePC, and tile products, Sustain Hardback and Sustain Cushion, have both been certified at the Silver Level under version\r\n2. Beauty. Service. Quality. Partnership. For over 30 years, these tenants have driven SustainCarpets - California's largest carpet design and manufacturing\r\ncorporation. Our award-winning broadloom, carpet tile and area rug products exude high performance and have earned superior Textile Appearance\r\nRetention Ratings (TARR), Cradle to Cradle, Green Label Plus certification and NSF-140 Gold certifications. SustainCarpets manufactures in a LEED for Existing\r\nBuildings Gold Certified facility and is a multi-year recipient of the GSA Evergreen Award. This products is Living Building Challenge Red List Free.\r\n",
        "csi_division": "09 Finishes",
        "csi_section": "09 68 13 Tile Carpeting ",
        "created": "2018-01-31 22:21:36",
        "updated": "2018-01-31 22:21:36",
        "record": 4632
      },
      "materials": [
        {
          "id": 30,
          "owner_id": 2,
          "name": "FACE YARN",
          "manufacturer": "HPD Collaborative",
          "created": "2015-11-17 14:44:42",
          "updated": "2015-11-17 14:44:42",
          "mask": 0,
          "min": "53.6000",
          "max": "0.0000",
          "alternate": 0,
          "reportable": 0,
          "hpd_url": "",
          "threshold": 4,
          "residuals": 0,
          "residual_notes": null,
          "notes": "",
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
      ],
      "reference": {
        "id": 3399,
        "address1": "1234 Street Rd",
        "address2": "",
        "city": "City of Sustainability",
        "state": "CA",
        "postal": "98210",
        "country": "USA",
        "website": "www.SustainCarpets.com",
        "contact": "Bruce Wayne",
        "title": "Sustainability Man",
        "phone": "555-555-5555",
        "email": "Bruce.wayne@ SustainCarpets.com",
        "created": "2018-01-31 22:21:36",
        "updated": "2018-01-31 22:21:36"
      },
      "vocs": {
        "id": 653,
        "voccontent": 1,
        "material": "3",
        "regulatory": "67",
        "exempt": 1,
        "ultra": 0,
        "created": "2018-03-27 23:29:57",
        "updated": "2018-03-27 23:29:57",
        "record": 4632
      },
      "accessories": [
        {
          "id": 1417,
          "name": "SUSTAIN 2300 ULTRA GREEN PLUS TILE ADHESIVE (VOC 0.00 G/L)",
          "website": "",
          "conditions": "Sustain Carpets recommended adhesive should be utilized to aid in the proper installation of Sustain Cushion Tile products and to ensure the product warranty.\r\n",
          "created": "2018-01-31 22:21:36",
          "updated": "2018-01-31 22:21:36"
        },
        ...
      ],
      "certifications": [
        {
          "id": 2896,
          "owner_id": 2,
          "type": "VOC emissions",
          "other_type": "",
          "name": "CRI Green Label Plus - Carpet",
          "voc": null,
          "party": "Second Party",
          "issue": "2013-06-30",
          "expire": "2015-06-30",
          "lab": "Carpet & Rug Institute (CRI)",
          "facilities": "All Facilities.",
          "website": "",
          "notes": "",
          "pharos_id": null,
          "created": "2018-01-31 22:21:36",
          "updated": "2018-01-31 22:21:36"
        },
        ...
      ],
      "summary": {
        "threshold": [
          4,
          4,
          4,
          4
        ],
        "considered": 0,
        "worstbm": "BM-1",
        "bm34": 1,
        "disclosed": 0,
        "screened": 0,
        "characterized": 0,
        "nano": "No",
        "residual_notes": 0,
        "leed1": 0,
        "leed2": 0,
        "leed_summary_messages": {
          "Residuals/Impurities Notes": "Residuals/Impurities notes are required for LEED Option 1 & 2",
          "GreenScreen": "BM-1, LT-1, and LT-P1 are not permissible GreenScreen scores for LEED Option 2.",
          "Screened": "Screening is required for Option 1 & 2.",
          "Characterized": "Characterized is required for Option 1 & 2.",
          "Threshold Level": "LEED Option 1 requires a minimum threshold level of 100 ppm or 1000 ppm.  LEED Option 2 requires a minimum threshold level of 100ppm."
        },
        "completeness": {
          "section1": {
            "successes": [],
            "errors": [],
            "warnings": []
          },
          "section2": {
            "successes": [],
            "errors": [],
            "warnings": {
              "Material HPD URL": "Some Material HPD URLs were blank.",
              "Residuals & Impurities Notes": "Residuals & Impurities Notes must be completed for each material.",
              "Other Material Notes": "Other Material or Product Notes must be completed for each material.",
              "Hazards": "Hazards not found for one or more substances.",
              "Substance Notes": "Notes not found for one or more substances.",
              "Materials": "One or more materials does not contain a substance."
            }
          },
          "section3": {
            "successes": [],
            "errors": [],
            "warnings": []
          },
          "section4": {
            "successes": [],
            "errors": [],
            "warnings": []
          },
          "section5": {
            "successes": [],
            "errors": [],
            "warnings": []
          },
          "section6": {
            "successes": [],
            "errors": [],
            "warnings": []
          },
          "errors": false,
          "warnings": true
        }
      }
    },
    ...
  ]
}
```

### Fetch a Record by ID {.doc-heading}

::: abstract requirements

- Endpoint: `/api/2.1/records/{id}/show`
- Method: `GET`
- Params:
  - Allowed: `record id in endpoint url`
  - Required: `record id in endpoint url`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/records/{id}/show \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `resource | 404`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 2101,
  "message": "Single record listing.",
  "data": {
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
```

### Filter a Record by ID {.doc-heading}

::: abstract requirements

- Endpoint: `/api/2.1/records/{id}/show`
- Method: `PUT`
- Params:
  - Allowed:
    - `(array)filters`
    - Available filters:
    - `(string)product` _(always includes company)_
    - `(string)owner`
    - `(string)format`
    - `(string)detail`
    - `(string)materials`
    - `(string)note`
    - `(string)substances` _(requires materials)_
    - `(string)reference`
    - `(string)vocs`
    - `(string)accessories`
    - `(string)certifications`
    - `(string)summary`
  - Required:
    - `At least one allowed filter`
    - `record id in endpoint url`

:::

Request:

```bash
curl --request PUT \
  --url API_URL/api/2.1/records/{id}/show \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ 'filters': ['product','owner','format','detail','materials','substances','reference','vocs','accessories','certifications','summary'] }"
```

Response returns: `resource | 404`

```json hl_lines="20 26 34 41 51 63 81 112 128 139 150 171"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 2107,
  "message": "Filtered single record listing.",
  "data": {
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
    "product": {
      "id": 2,
      "name": "Cushion Tile by Sustain Carpets",
      "archived": false,
      "created": "2015-11-10 22:20:17",
      "updated": "2015-11-10 22:20:17",
      "company": {
        "id": 2,
        "name": "HPD Collaborative",
        "archived": 0,
        "created": "2015-11-07 02:13:28",
        "updated": "2015-11-07 02:13:28"
      }
    },
    "owner": {
      "id": 2,
      "name": "HPD Collaborative",
      "archived": 0,
      "created": "2015-11-07 02:13:28",
      "updated": "2015-11-07 02:13:28"
    },
    "format": {
      "id": 4,
      "name": "Health Product Declaration",
      "version": "2.1",
      "abbreviation": "HPD",
      "publishable": 1,
      "archived": 0,
      "created": "2017-08-01 02:37:07",
      "updated": "2017-08-01 02:37:07"
    },
    "detail": {
      "id": 4306,
      "classification": "09 68 13 Tile Carpeting ",
      "description": "This HPD covers all products on Sustain Carpet’s Sustain® Cushion Tile. Products construction includes Nylon 6,6 face fiber, thermoplastic laminate, polyurethane cushion and Sustain® scrim.",
      "threshold_type": "Material",
      "inventory_notes": "This product has undergone the Cradle to Cradle Certification™ material health evaluation and has achieved Silver level certification. The assessment is\r\nconducted by an accredited assessor with expertise in toxicology and chemistry. Companies pursuing certification commit to phasing out problematic\r\ningredients that have been identified. The material health score indicates how much progress has been made in optimizing the product. Sustain’s standard\r\nbroadloom, High PerformancePC, and tile products, Sustain Hardback and Sustain Cushion, have both been certified at the Silver Level under version\r\n2. Beauty. Service. Quality. Partnership. For over 30 years, these tenants have driven SustainCarpets - California's largest carpet design and manufacturing\r\ncorporation. Our award-winning broadloom, carpet tile and area rug products exude high performance and have earned superior Textile Appearance\r\nRetention Ratings (TARR), Cradle to Cradle, Green Label Plus certification and NSF-140 Gold certifications. SustainCarpets manufactures in a LEED for Existing\r\nBuildings Gold Certified facility and is a multi-year recipient of the GSA Evergreen Award. This products is Living Building Challenge Red List Free.\r\n",
      "csi_division": "09 Finishes",
      "csi_section": "09 68 13 Tile Carpeting ",
      "created": "2018-01-31 22:21:36",
      "updated": "2018-01-31 22:21:36",
      "record": 4632
    },
    "materials": [
      {
        "id": 30,
        "owner_id": 2,
        "name": "FACE YARN",
        "manufacturer": "HPD Collaborative",
        "created": "2015-11-17 14:44:42",
        "updated": "2015-11-17 14:44:42",
        "mask": 0,
        "min": "53.6000",
        "max": "0.0000",
        "alternate": 0,
        "reportable": 0,
        "hpd_url": "",
        "threshold": 4,
        "residuals": 0,
        "residual_notes": null,
        "notes": "",
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
    ],
    "reference": {
      "id": 3399,
      "address1": "1234 Street Rd",
      "address2": "",
      "city": "City of Sustainability",
      "state": "CA",
      "postal": "98210",
      "country": "USA",
      "website": "www.SustainCarpets.com",
      "contact": "Bruce Wayne",
      "title": "Sustainability Man",
      "phone": "555-555-5555",
      "email": "Bruce.wayne@ SustainCarpets.com",
      "created": "2018-01-31 22:21:36",
      "updated": "2018-01-31 22:21:36"
    },
    "vocs": {
      "id": 653,
      "voccontent": 1,
      "material": "3",
      "regulatory": "67",
      "exempt": 1,
      "ultra": 0,
      "created": "2018-03-27 23:29:57",
      "updated": "2018-03-27 23:29:57",
      "record": 4632
    },
    "accessories": [
      {
        "id": 1417,
        "name": "SUSTAIN 2300 ULTRA GREEN PLUS TILE ADHESIVE (VOC 0.00 G/L)",
        "website": "",
        "conditions": "Sustain Carpets recommended adhesive should be utilized to aid in the proper installation of Sustain Cushion Tile products and to ensure the product warranty.\r\n",
        "created": "2018-01-31 22:21:36",
        "updated": "2018-01-31 22:21:36"
      },
      ...
    ],
    "certifications": [
      {
        "id": 2896,
        "owner_id": 2,
        "type": "VOC emissions",
        "other_type": "",
        "name": "CRI Green Label Plus - Carpet",
        "voc": null,
        "party": "Second Party",
        "issue": "2013-06-30",
        "expire": "2015-06-30",
        "lab": "Carpet & Rug Institute (CRI)",
        "facilities": "All Facilities.",
        "website": "",
        "notes": "",
        "pharos_id": null,
        "created": "2018-01-31 22:21:36",
        "updated": "2018-01-31 22:21:36"
      },
      ...
    ],
    "summary": {
      "threshold": [
        4,
        4,
        4,
        4
      ],
      "considered": 0,
      "worstbm": "BM-1",
      "bm34": 1,
      "disclosed": 0,
      "screened": 0,
      "characterized": 0,
      "nano": "No",
      "residual_notes": 0,
      "leed1": 0,
      "leed2": 0,
      "leed_summary_messages": {
        "Residuals/Impurities Notes": "Residuals/Impurities notes are required for LEED Option 1 & 2",
        "GreenScreen": "BM-1, LT-1, and LT-P1 are not permissible GreenScreen scores for LEED Option 2.",
        "Screened": "Screening is required for Option 1 & 2.",
        "Characterized": "Characterized is required for Option 1 & 2.",
        "Threshold Level": "LEED Option 1 requires a minimum threshold level of 100 ppm or 1000 ppm.  LEED Option 2 requires a minimum threshold level of 100ppm."
      },
      "completeness": {
        "section1": {
          "successes": [],
          "errors": [],
          "warnings": []
        },
        "section2": {
          "successes": [],
          "errors": [],
          "warnings": {
            "Material HPD URL": "Some Material HPD URLs were blank.",
            "Residuals & Impurities Notes": "Residuals & Impurities Notes must be completed for each material.",
            "Other Material Notes": "Other Material or Product Notes must be completed for each material.",
            "Hazards": "Hazards not found for one or more substances.",
            "Substance Notes": "Notes not found for one or more substances.",
            "Materials": "One or more materials does not contain a substance."
          }
        },
        "section3": {
          "successes": [],
          "errors": [],
          "warnings": []
        },
        "section4": {
          "successes": [],
          "errors": [],
          "warnings": []
        },
        "section5": {
          "successes": [],
          "errors": [],
          "warnings": []
        },
        "section6": {
          "successes": [],
          "errors": [],
          "warnings": []
        },
        "errors": false,
        "warnings": true
      }
    }
  }
}
```

### Create a New Record {.doc-heading}

::: abstract requirements

- Endpoint: `/api/2.1/records/{id}`
- Action: `POST`
- Params:
  - Allowed:
    - `product id in endpoint url`
    - `(int)inventory_type`
    - `(int)residuals`
  - select from:
    - 0: Not Considered
    - 1: Considered
    - 2: Partially Considered
    - `(text)residual_notes`
  - Required:
    - `product id in endpoint url` \* `(int)inventory_type`

:::

Request:

```bash
curl --request POST \
  --url API_URL/api/2.1/records/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{ "inventory_type": 4 | 5 }'
```

Response returns: `resource | validation errors`

::: tip
Inventory type 5, a Basic Record, will also create a Material and Detail resource and return those with the new Record resource.

    If you're creating your Record in Steps, you should store the returned `id` field in your application as it will be used when creating all other properties of your Record.

:::

Inventory type 4 - Nested:

```json hl_lines="20 26"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 2102,
  "message": "Record created successfully.",
  "data": {
    "id": 4914,
    "format_id": 4,
    "stage_id": 3,
    "archived": false,
    "created": "2018-03-29 10:04:22",
    "updated": "2018-03-29 10:04:22",
    "published_filename": null,
    "published_at": null,
    "screened": "2018-03-29 10:04:22",
    "inventory_type": 4,
    "leed_calc": false,
    "leed_display": false,
    "no_accessory": false,
    "product": {
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
      }
    }
  }
}
```

Inventory type 5 - Basic:

```json hl_lines="20 26 34 46"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 2102,
  "message": "Record created successfully.",
  "data": {
    "id": 4916,
    "format_id": 4,
    "stage_id": 3,
    "archived": false,
    "created": "2018-03-29 10:10:49",
    "updated": "2018-03-29 10:10:49",
    "published_filename": null,
    "published_at": null,
    "screened": "2018-03-29 10:10:49",
    "inventory_type": 5,
    "leed_calc": false,
    "leed_display": false,
    "no_accessory": false,
    "product": {
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
      }
    },
    "detail": {
      "id": 4597,
      "classification": null,
      "description": null,
      "threshold_type": "Product",
      "inventory_notes": null,
      "csi_division": null,
      "csi_section": null,
      "created": "2018-03-29 10:10:49",
      "updated": "2018-03-29 10:10:49",
      "record": 4916
    },
    "materials": [
      {
        "id": 6955,
        "owner_id": 2,
        "name": "Test Product",
        "manufacturer": "2",
        "created": "2018-03-29 10:10:49",
        "updated": "2018-03-29 10:10:49",
        "mask": 0,
        "min": "100.0000",
        "max": "100.0000",
        "alternate": 0,
        "reportable": 0,
        "hpd_url": null,
        "threshold": 5,
        "residuals": 0,
        "residual_notes": null,
        "notes": null
      }
    ]
  }
}
```
