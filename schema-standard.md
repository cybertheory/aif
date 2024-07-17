# Schema Standard

## 1. Schema Format

Schemas should be defined using JSON Schema (draft-07 or later).

## 2. Versioning

Schemas must include a version number in the format: `vX.Y.Z`

## 3. Required Fields

All schemas must include:

- `$schema`: URL of the JSON Schema draft used
- `$id`: Unique identifier for the schema
- `title`: Human-readable name of the schema
- `type`: The base type of the schema (usually "object")
- `properties`: Define the structure of the object

## 4. Example Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "https://example.com/schemas/user.json",
  "title": "User",
  "version": "v1.0.0",
  "type": "object",
  "properties": {
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "email": {
      "type": "string",
      "format": "email"
    }
  },
  "required": ["id", "name", "email"]
}
```

## 5. Schema Retrieval API
- Systems must expose an endpoint for schema retrieval:
```
GET /api/v1/schemas
```
- Response should be a list of available schemas with their versions.