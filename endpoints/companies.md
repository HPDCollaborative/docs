---
title: Company Endpoints
description: Instructions, endpoints and examples for the Companies resource group.
category: Developer Guide
---

# {{ $frontmatter.title }}

[[toc]]

The Companies resource group contains a single endpoint to assist in the creation of an active company select menu for use in your UI. Response is truncated for brevity.

### List Active Companies

::: abstract requirements

- Endpoint: `/api/2.1/companies`
- Method: `GET`
- Params:
- Allowed | Required: `NULL`

:::

Request:

```bash
--url API_URL/api/2.1/companies \
  --header 'authorization: Bearer TOKEN' \
  --header 'Content-Type: application/json' \
```

Response returns: `collection | null`

```json
{
  "http_status": 200,
  "http_message": "OK",
  "status": 9002,
  "message": "List of active Companies.",
  "data": [
    {
      "id": 1,
      "name": "Healthy Building Network"
    },
    {
      "id": 2,
      "name": "HPD Collaborative"
    },
    {
      "id": 3,
      "name": "Leap Innovation LLC"
    },
   ...
  ]
}
```
