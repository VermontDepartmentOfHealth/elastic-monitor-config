
## Elastic Beats

* [Monitor Options Docs](https://www.elastic.co/guide/en/beats/heartbeat/current/configuration-heartbeat-options.html#monitor-schedule)
  * [Monitor Options Doc Source](https://github.com/elastic/beats/blob/master/heartbeat/docs/heartbeat-options.asciidoc)
* [Yaml Tips & Gotchas](https://www.elastic.co/guide/en/beats/heartbeat/current/yaml-tips.html)
* [heartbeat.reference.yml](https://github.com/elastic/beats/blob/master/heartbeat/heartbeat.reference.yml)
* 
## Yaml Validation in VS Code

* [Schema Validation for YAML](https://json-schema-everywhere.github.io/yaml)
* [YAML - Red Hat](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml)
  * [redhat-developer/vscode-yaml](https://github.com/redhat-developer/vscode-yaml)
* [vscode-yaml-validation](https://github.com/djabraham/vscode-yaml-validation)


## JSON Schema Definition

* [SchemaStore - Schemas](http://schemastore.org/json/)
  * [schemastore on github](https://github.com/schemastore/schemastore/)
* [JSON Schema Validator](https://www.jsonschemavalidator.net/)

[Mapping to a schema defined in settings](https://code.visualstudio.com/docs/languages/json#_mapping-to-a-schema-in-the-workspace)

```json
"json.schemas": [
    {
        "fileMatch": [
            "monitors.d/*.json"
        ],
        "url": "./heartbeat-schema.json"
    }
]
```

[Structuring a complex schema](https://json-schema.org/understanding-json-schema/structuring.html)

```json
{ "$ref": "definitions.json#/address" }
```

[JsonSchema - conditionally require attribute](https://stackoverflow.com/a/38781027/1366033)


[Applying subschemas conditionally](https://json-schema.org/understanding-json-schema/reference/conditionals.html)

```json
{
  "type": "object",
  "properties": {
    "street_address": {
      "type": "string"
    },
    "country": {
      "enum": ["United States of America", "Canada"]
    }
  },
  "if": {
    "properties": { "country": { "const": "United States of America" } }
  },
  "then": {
    "properties": { "postal_code": { "pattern": "[0-9]{5}(-[0-9]{4})?" } }
  },
  "else": {
    "properties": { "postal_code": { "pattern": "[A-Z][0-9][A-Z] [0-9][A-Z][0-9]" } }
  }
}
```

[URL Validaiton / Format](https://github.com/json-schema-org/json-schema-spec/issues/233#issuecomment-279180514)

```json
{
    "type": "string",
    "format": "uri",
    "pattern": "^(https?|wss?|ftp)://"
}
```


[JsonSchema - Array](https://cswr.github.io/JsonSchema/spec/arrays/)

```json
{
    "type": "array",
    "items": {
        "type": "string"
    }
}
```


[JsonSchema - String](https://json-schema.org/understanding-json-schema/reference/string.html)

```json
{ "type": "string" }
```


[Using RegEx in JSON Schema](https://stackoverflow.com/q/16491973/1366033)

```json
"phone": {
    "type": "string",
    "pattern": "^(\\([0-9]{3}\\))?[0-9]{3}-[0-9]{4}$"
}
```