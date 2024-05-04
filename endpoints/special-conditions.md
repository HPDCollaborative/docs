---
title: Special Condition Endpoints
description: Instructions, endpoints and examples for special conditions.
category: Developer Guide
---

[[toc]]

# {{ $frontmatter.title }}

Special Conditions were implemented starting at version 2.1.1 of the HPD Open Standard. For more information on when to use Special Conditions in your HPD see the [documentation here.](https://www.hpd-collaborative.org/special-conditions)

This page will cover both Special Condition Materials and Special Condition Substances as well as the Selectable Options for Special Conditions for use in your own UI.

## 1. Selectable Options

> [!note]
> Use this endpoint to create a select menu or radio buttons for selecting the appropriate Special Condition for your Material or Substance. These condition ids are the same for both Materials and Substances.

::: abstract requirements

- Endpoint: `/api/2.1/special-condition/options`
- Method: `GET`
- Params: `none`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/special-condition/options \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `array`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 9100,
  "message": "Special Conditions selectable options.",
  "data": {
    "1": "Biological Material",
    "2": "Geological Material",
    "3": "Mixed Recycled Content",
    "4": "Electronics"
  }
}
```

## Add a Special Condition Material to a Record

> [!danger] important
> When created your UI for adding a Special Condition Material, it's important to provide the user with a select menu or other method to select from existing Materials, and to select the appropriate Special Condition (see above). You will also need to provide a text field so that they can create a new Material. If a `material_id` is not passed to the API, then a `name` field is required.

::: abstract requirements

- Endpoint: `/api/2.1/special-condition/material/{id}`
- Method: `POST`
- Params:
  - Allowed:
    - `(int)material_id`
    - `(string)name`
    - `(decimal)min`
    - `(decimal)max`
    - `(bool)mask`
    - `(bool)alternate`
    - `(bool)unreportable`
    - `(string)hdp_url`
    - `(int)threshold`
    - `(text)notes`
    - `(text)residual_notes`
  - Required:
    - `(int)condition_id`
    - `(string)name (only required IF no material_id is passed)`
    - `(decimal)min`
    - `(bool)residuals`
    - `record id in endpoint url`

:::

Request:

```bash
curl --request POST \
  --url API_URL/api/2.1/special-condition/material/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ condition_id: 1, name: 'API Test Special Condition Material', mask: 0, min: 35, max: 55, alternate: 1, unreportable: 1, hpd_url: 'http://example.com', threshold: 3, residuals: 1, residual_notes: 'Test residual notes for this testing material.', notes: 'Test notes' }"
```

Response returns: `resource | validation errors`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 9101,
  "message": "Special Condition material created successfully.",
  "data": {
    "id": 9924,
    "owner_id": 2,
    "name": "SC:Bio:API Test Special Condition Material",
    "manufacturer": "HPD Collaborative",
    "created": "2019-01-14 21:53:24",
    "updated": "2019-01-14 21:53:24",
    "alternate": 1,
    "reportable": 1,
    "hpd_url": "http://example.com",
    "threshold": 3,
    "residuals": 1,
    "residual_notes": "Test residual notes for this testing material."
  }
}
```

## Add a Special Condition Substance to a Material

> [!danger] important
> Special Condition substances utilize a single array field `payload` to store the data corresponding to the passed in `condition_id`. These values vary based on the condition. Please make double sure that you pass in the correct set of values under the `payload` field as references in section 4 below.

::: abstract requirements

- Endpoint: `/api/2.1/special-condition/substance`
- Method: `POST`
- Params:
  - Optional:
    - `(boolean)mask`
    - `(decimal)max`
    - `(boolean)residual`
    - `(text)notes`
  - Required:
    - `(string)name`
    - `(integer)record_id`
    - `(integer)material_id`
    - `(integer)condition_id`
    - `(array)payload` _(see Section 4 below)_
    - `(decimal)min`
    - `(string)role`
    - `(integer)nano` _(0 = No, 1 = Yes, 2 = Unknown)_
    - `(string)recycle` _(select one - Both, PostC, PreC, None, UNK)_

:::

Request:

```bash
curl --request POST \
  --url API_URL/api/2.1/special-condition/substance \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
  --data "{ record_id: 6023, material_id: 9925, name: 'Test Electronic Substance', condition_id: 4, payload: { elect: { description: 'Here is a brief description.', compliance: 'Is compliant.', takeback: 'Not eligible for takeback.' }}, mask: false, min: '100.00', max: '100.00', residual: '', nano: '0', role: 'Mixer', recycle: 'None', notes: '' }"
```

Response returns: `resource | validation errors`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 9102,
  "message": "Special condition substance was added successfully.",
  "data": {
    "id": 49362,
    "owner_id": 2,
    "name": "Test Electronic Substance",
    "cas": "SC:Electronics",
    "material_id": 9925,
    "pharos_id": null,
    "gslt": "Not Screened",
    "nocas": false,
    "biobased": false,
    "created": "2019-01-15 00:14:00",
    "updated": "2019-01-15 00:14:00",
    "screened": 0,
    "nocasorid": false,
    "noid": false,
    "nohazard": false,
    "hazards": []
  }
}
```

## Payload Params by Condition ID

> [!note]
> As referenced above each condition has different parameters that must be passed as the `payload` field. These values are expressed below in JSON format, please convert these values to arrays for whichever language you're using in your application.

### Biological Material

::: abstract requirements

- **Category** (required)
  - Live micro-organisms - includes fungi, bacteria, and other micro-organisms.
  - Live plants - any member of the kingdom Plantae in it's live state.
  - Tree-based materials
  - Plant-based materials
  - Animal-based materials
  - Microbial tissue based materials
  - Plant. animal, and microbe-derived mixtures
- **Identifier** (required)
  - Enter the most specific identifier available. Depending on the category, this may be the scientific name (genus species or genus sp, or species of the fungal mycelium) or another identifier.

:::

Request:

```json
payload: {
	bio: {
		category: (int) Choose from 1-7 above,
		identifier: (string)'text',
	}
}
```

#### Geological Material

::: abstract requirements

- **Origin** (required) - Country and, if available, exact location of quarry / extraction area.
- **Typical Composition** - If available.
- **Potential Presence of Toxic Materials** - Defined as antimony, arsenic, cadmium, chromium VI, cobalt, lead, mercury, nickel, thallium, tin, uranium, and vanadium.
- **Presence of Radioactive Elements** - For rock or stone based materials (e.g., sandstone, slate, granite) provide available information on the presence of radioactive elements, namely radium, thorium, and potassium 40 (K40).

:::

```json
payload: {
	geo: {
		origin: (string)'text',
		typical: (string)'text',
		potential: (string)'text',
		presence: (string)'text',
	}
}
```

#### Mixed Recycled Content

::: abstract requirements

- **Testing**
  - Is regular, analytical testing performed on the substance? (required)
  - Yes
  - No
- **Testing Text**
  - This content should be based on what was selected in the `testing` value.
  - If Yes is selected include the following information:
  - Test method(s) employed.
  - List of chemicals and/or elements (including those of a hazardous nature) that are covered by the testing.
  - Name and accredidation of the lab(s) that perform the testing.
  - Representative material sample covered by the testing.
  - If No is selected:
  - Describe how the substance was inventoried (manufacturer/supplier attestation or other)?
- **Variation**
  - Is there any batch variation for the substances? What are the causes of the variation?
- **Country**
  - What is the source or country of origin for the substance?
- **Info**
  - Why is there limited information or a lack thereof?

:::

```json
payload: {
	mixed: {
		testing: (int) Choose from 1 Yes or 2 No,
		testing_text: (string)'text',
		variation: (string)'text',
		country: (string)'text',
		info: (string)'text',
	}
}
```

#### Electronics

::: abstract requirements

- **Brief Description**
  - Enter a brief description of the component or part (including it's function).
- **Compliance**
  - Indicate if the component or part is compiant with the most recent EU RoHS directive without any exemption, or with [fill in] exemptions.
- **Takeback Program**
  - Include a statement that the component is/isn't included in a takeback program.

:::

```json
payload: {
	elect: {
		description: (string)'text',
		compliance: (string)'text',
		takeback: (string)'text',
	}
}
```
