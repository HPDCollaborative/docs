---
title: Completeness Summary
description: Instructions, endpoints and examples for the Summary resource group.
---

[[toc]]

# Completeness Summary {.doc-heading}

The Completeness Summary provides you with a simple array to show which items still require attention. You can create a simple modal component in your UI to display this to your users.

### List Summary by Record ID {.doc-heading}

::: abstract requirements

- Endpoint: `/api/2.1/summary/{id}`
- Method: `GET`
- Params:
  - Allowed: `record id in endpoint url`
  - Required: `record id in endpoint url`

:::

Request:

```bash
curl --request GET \
  --url API_URL/api/2.1/summary/{id} \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `array | null`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 9003,
  "message": "Completeness Summary for Record.",
  "data": {
    "threshold": [4, 4, 3, 3, 3, 3, 3, 3, 3, 4, 3, 4, 4],
    "considered": 8,
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
      "Threshold Level": "LEED Option 1 requires a minimum threshold level of 100 ppm or 1000 ppm.  LEED Option 2 requires a minimum threshold level of 100ppm.",
      "Completeness": "All data fields required in section 4.0 of the HPD Open Standard are required for Option 1 & 2.  Please see the record page for more info."
    },
    "completeness": {
      "section1": {
        "successes": [],
        "errors": [],
        "warnings": []
      },
      "section2": {
        "successes": [],
        "errors": {
          "Role": "Role is required for all substances."
        },
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
      "errors": true,
      "warnings": true
    }
  }
}
```
