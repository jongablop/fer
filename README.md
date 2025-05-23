# ``fer``: Framework for Experimental Results

## Data structure
We have developed a JSON schema for the ``fer`` data structure that includes the main and auxiliary data structures (such as QuantityValues, Measurement, and Source) and respects the nested relationships between them. You can download it from [here](https://github.com/jongablop/fer/blob/main/fer-schema.json).

<details>

<summary>See JSON schema</summary>

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "FER Data Structure",
  "description": "Schema for experimental result file following the 'fer' data structure.",
  "type": "object",
  "properties": {
    "quantity_values": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": { "type": "string" },
          "name": { "type": "string" },
          "description": { "type": "string" },
          "changelog": {
            "type": "array",
            "items": { "$ref": "#/definitions/ChangelogEntry" }
          },
          "quantities": {
            "type": "array",
            "items": { "type": "string" }
          },
          "symbols": {
            "type": "array",
            "items": { "type": "string" }
          },
          "units": {
            "type": "array",
            "items": { "type": "string" }
          },
          "values": {
            "type": "array",
            "items": {
              "type": "array",
              "items": { "type": "number" }
            }
          },
          "standard_uncertainties": {
            "type": "array",
            "items": {
              "type": "array",
              "items": { "type": "number" }
            }
          },
          "coverages": {
            "type": "array",
            "items": { "$ref": "#/definitions/Coverage" }
          },
          "probability_density_functions": {
            "type": "array",
            "items": { "$ref": "#/definitions/ProbabilityDensityFunction" }
          },
          "correlation_indices": {
            "type": "array",
            "items": { "type": "integer" }
          }
        },
        "required": ["id", "name", "quantities", "units", "values", "standard_uncertainties"]
      }
    },
    "measurement": {
      "type": "object",
      "properties": {
        "id": { "type": "string" },
        "changelog": {
          "type": "array",
          "items": { "$ref": "#/definitions/ChangelogEntry" }
        },
        "description": { "type": "string" },
        "correct": { "type": "boolean" },
        "state": { "$ref": "#/definitions/State" },
        "results": {
          "type": "array",
          "items": { "$ref": "#/definitions/QuantityValues" }
        },
        "correlations": { "$ref": "#/definitions/Correlations" },
        "measurands": {
          "type": "array",
          "items": { "type": "string" }
        },
        "source": { "$ref": "#/definitions/Source" }
      },
      "required": ["id", "results", "source"]
    },
    "source": {
      "type": "object",
      "properties": {
        "id": { "type": "string" },
        "name": { "type": "string" },
        "description": { "type": "string" },
        "model": { "type": "string" },
        "influence_quantities": {
          "type": "array",
          "items": { "$ref": "#/definitions/QuantityValues" }
        },
        "input_quantities": {
          "type": "array",
          "items": { "$ref": "#/definitions/Measurement" }
        },
        "correlations": { "$ref": "#/definitions/Correlations" }
      },
      "required": ["id", "name", "input_quantities"]
    }
  },
  "definitions": {
    "ChangelogEntry": {
      "type": "object",
      "properties": {
        "timestamp": { "type": "string", "format": "date-time" },
        "user": { "type": "string" },
        "description": { "type": "string" }
      },
      "required": ["timestamp", "description"]
    },
    "State": {
      "type": "object",
      "properties": {
        "name": { "type": "string" },
        "description": { "type": "string" },
        "quantity_value": { "$ref": "#/definitions/QuantityValues" }
      }
    },
    "ProbabilityDensityFunction": {
      "type": "object",
      "properties": {
        "name": { "type": "string" },
        "parameters": {
          "type": "array",
          "items": { "type": "string" }
        },
        "values": {
          "type": "array",
          "items": { "type": "number" }
        }
      },
      "required": ["name", "parameters", "values"]
    },
    "Correlations": {
      "type": "object",
      "properties": {
        "quantities": {
          "type": "array",
          "items": { "type": "string" }
        },
        "correlation_matrix": {
          "type": "array",
          "items": {
            "type": "array",
            "items": { "type": "number" }
          }
        },
        "method": { "type": "string" }
      }
    },
    "Coverage": {
      "type": "object",
      "properties": {
        "intervals": {
          "type": "array",
          "items": {
            "type": "array",
            "items": { "type": "number" }
          }
        },
        "probabilities": {
          "type": "array",
          "items": { "type": "number" }
        },
        "degrees_of_freedom": {
          "type": "array",
          "items": { "type": "integer" }
        },
        "method": { "type": "string" }
      }
    }
  }
}
```

</details>

### Examples

## Implementations

A Python-based implementation of the fer data structure can be found [here](https://github.com/jongablop/ferpy).
