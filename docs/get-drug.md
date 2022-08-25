---
sidebar_position: 2
slug: /get-drug
---

# Getting Generic Suggestions for a Drug

This endpoint allows you to pull information on a specific drug resource inside a specific formulary.

Root URL: `https://agostinis-fms/api/v1`

Endpoint: `/formulary/[formulary_id]/drug/[drug_ndc]`

Route parameters:

| Parameter      | Meaning                                                                | Example Value   |
| -------------- | ---------------------------------------------------------------------- | --------------- |
| `formulary_id` | The ID of the specific formulary that you want to pull drug data from. | `agostinis-ltd` |
| `drug_ndc`     | The NDC of the specific drug that you want to get information for.     | `0310-0751-90`  |

## Possible Responses

Response schema:

| Field Name                     | Data Type       | Comment                                                                                                                                     |
| ------------------------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `found_formulary`              | `boolean`       | Value is `true` if a formulary was found for the specified `formulary_id`                                                                   |
| `found_drug`                   | `boolean`       | Value is `true` if a drug was found for the specified `drug_id`                                                                             |
| `branded`                      | `boolean`       | Value is `true` if the drug is branded                                                                                                      |
| `suggestion?`                  | `map` or `null` | If the drug is branded, we will send back generic suggestions here. This value is `null` if there are no generic suggestions for this drug. |
| `suggestion?.prompt`           | `map`           | This will contain content for the formatting of the popup bubble which will prompt the pharmacist.                                          |
| `suggestion?.generic_drugs`    | `array<drug>`   | This will contain the generic drug suggestions. Please see below for how the `drug` data type is formatted.                                 |
| `suggestion?.generic_drugs[n]` | `drug`          |                                                                                                                                             |

|

### Found formulary, found drug & found generics for drug

Example response:

```
  {
    "found_formulary": boolean,
    "found_drug": boolean,
    "branded": true,
    "suggestion": {
      "prompt": {

      }
    }
  }
```

## Error Cases

### Missing `formulary_id` route parameter

Response will contain a `400` status code.

### Missing `drug_ndc` route parameter

Response will contain a `400` status code.

### Invalid `formulary_id` route parameter

If the server is unable to find any formularies for the given `formulary_id`, we will
send back a `404` status code.

### Invalid `drug_ndc` route parameter

If a drug is

If the server is unable to find any drugs for the given `formulary_id`, we will
send back a `404` status code.
