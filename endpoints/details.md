---
title: Detail Endpoints
description: Instructions, endpoints and examples for the Detail model.
category: Developer Guide
---

[[toc]]

# {{ $frontmatter.title }}

> [!note]
> Response variables have been truncated for brevity.

### List Detail by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/details/{id}`
- Method: `GET`
- Params:
  - Allowed: `record id in endpoint url`
  - Required: `record id in endpoint url`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/details/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `resource | 404`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 9501,
  "message": "Details listing for record.",
  "data": {
    "id": 4306,
    "classification": "09 68 13 Tile Carpeting ",
    "description": "This HPD covers all products on ...",
    "threshold_type": "Material",
    "inventory_notes": "This product has undergone the Cradle to ...",
    "csi_division": "09 Finishes",
    "csi_section": "09 68 13 Tile Carpeting ",
    "created": "2018-01-31 22:21:36",
    "updated": "2018-04-27 11:31:33",
    "record": 4632
  }
}
```

### Filter Detail by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/details/{id}`
- Method: `PUT`
- Params:
  - Allowed:
    - `(array)filters`
  - Available Filters:
    - `(string)record`
  - Required:
    - `at least one available filter`
    - `record id in endpoint url`

:::

Request:

```bash
curl --request PUT \
  --url API_URL/api/2.1/details/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ 'filters': ['record'] }" \
```

Response returns: `resource | error`

```json hl_lines="16"
{
  "http_status": 200,
  "http_message": "OK",
  "status": 9502,
  "message": "Filtered detail listing.",
  "data": {
    "id": 5604,
    "classification": "09 68 13 Tile Carpeting",
    "description": "This HPD covers all products on Sustain Carpet’s Sustain® Cushion Tile. Products construction includes Nylon 6,6 face fiber, thermoplastic laminate, polyurethane cushion and Sustain® scrim.",
    "threshold_type": "Product - 1,000 ppm",
    "inventory_notes": "This product has undergone the Cradle to Cradle Certification™ material health evaluation and has achieved Silver level certification. The assessment is\r\nconducted by an accredited assessor with expertise in toxicology and chemistry. Companies pursuing certification commit to phasing out problematic\r\ningredients that have been identified. The material health score indicates how much progress has been made in optimizing the product. Sustain’s standard\r\nbroadloom, High PerformancePC, and tile products, Sustain Hardback and Sustain Cushion, have both been certified at the Silver Level under version\r\n2. Beauty. Service. Quality. Partnership. For over 30 years, these tenants have driven SustainCarpets - California's largest carpet design and manufacturing\r\ncorporation. Our award-winning broadloom, carpet tile and area rug products exude high performance and have earned superior Textile Appearance\r\nRetention Ratings (TARR), Cradle to Cradle, Green Label Plus certification and NSF-140 Gold certifications. SustainCarpets manufactures in a LEED for Existing\r\nBuildings Gold Certified facility and is a multi-year recipient of the GSA Evergreen Award. This products is Living Building Challenge Red List Free.",
    "csi_division": "09 Finishes",
    "csi_section": "09 68 13 Tile Carpeting",
    "created": "2018-07-10 21:44:03",
    "updated": "2018-10-15 07:43:58",
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

### Add Data to Detail by Record ID

::: abstract requirements

- Endpoint: `/api/2.1/details/{id}`
- Method: `POST`
- Params:
  - Allowed:
    - `(string)classification`
    - `(text)description`
    - `(string)threshold_type`
    - `(text)inventory_notes`
    - `(string)csi_division`
    - `(string)csi_section`
  - Required:
    - `(string)classification`
    - `(text)description`
    - `(string)csi_division`
    - `(string)csi_section`
    - `record id in endpoint url`

:::

Request:

```bash
curl --request POST \
  --url API_URL/api/2.1/details/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{ "classification": "09 68 13 Tile Carpeting ", "description": "This HPD covers all products on ...", "threshold_type": "Material", "inventory_notes": "This product has undergone the Cradle to ...", "csi_division": "09 Finishes", "csi_section": "09 68 13 Tile Carpeting" }' \
```

Response returns: `resource | error`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 9504,
  "message": "Detail created successfully.",
  "data": {
    "id": 5604,
    "classification": "09 68 13 Tile Carpeting",
    "description": "This HPD covers all products on ...",
    "threshold_type": "Material",
    "inventory_notes": "This product has undergone the Cradle to ...",
    "csi_division": "09 Finishes",
    "csi_section": "09 68 13 Tile Carpeting",
    "created": "2018-07-10 21:44:03",
    "updated": "2019-08-12 16:33:03",
    "record": 6023
  }
}
```
