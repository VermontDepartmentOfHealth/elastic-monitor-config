
## Elastic Beats

* [Monitor Options Docs](https://www.elastic.co/guide/en/beats/heartbeat/current/configuration-heartbeat-options.html#monitor-schedule)
  * [Monitor Options Doc Source](https://github.com/elastic/beats/blob/master/heartbeat/docs/heartbeat-options.asciidoc)
* [Yaml Tips & Gotchas](https://www.elastic.co/guide/en/beats/heartbeat/current/yaml-tips.html)
* [heartbeat.reference.yml](https://github.com/elastic/beats/blob/master/heartbeat/heartbeat.reference.yml)


## Yaml Validation in VS Code

* [Schema Validation for YAML](https://json-schema-everywhere.github.io/yaml)
* [YAML - Red Hat](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml)
  * [redhat-developer/vscode-yaml](https://github.com/redhat-developer/vscode-yaml)
* [vscode-yaml-validation](https://github.com/djabraham/vscode-yaml-validation)
* [Autocompletion not showing up with conditional subschemas #222](https://github.com/redhat-developer/vscode-yaml/issues/222)

## Chron Syntax / Regex

[cron](https://en.wikipedia.org/wiki/Cron)
[cronexpr](https://github.com/gorhill/cronexpr#implementation)
[cron editor](https://github.com/gorhill/cronexpr#implementation)

[Create a regular expression for Cron statement](https://stackoverflow.com/q/14203122/1366033)


**General Format**


| Field name    | Mandatory? | Allowed values  | Special characters |
| ------------- | ---------- | --------------- | ------------------ |
| Seconds       | No*        | 0-59            | * / , -            |
| Minutes       | Yes        | 0-59            | * / , -            |
| Hours         | Yes        | 0-23            | * / , -            |
| Day of month  | Yes        | 1-31            | * / , - L W        |
| Month         | Yes        | 1-12 or JAN-DEC | * / , -            |
| Day of week   | Yes        | 0-6 or SUN-SAT  | * / , - L #        |
| Year          | No*        | 1970–2099       | * / , -            |


**Predefined Scheduling Macros**:


| Entry      | Equivalent to |
| ---------- | ------------- |
| @annually  | 0 0 0 1 1 * * |
| @yearly    | 0 0 0 1 1 * * |
| @monthly   | 0 0 0 1 * * * |
| @weekly    | 0 0 0 * * 0 * |
| @daily     | 0 0 0 * * * * |
| @hourly    | 0 0 * * * * * |
| @reboot    |               |


**Valid time units**:

| unit   | definition  |
| -------| ----------- |
| ns     | nanosecond  |
| us, µs | microsecond |
| ms     | millisecond |
| s      | second      |
| m      | minute      |
| h      | hour        |



[Regex to allow only number between 1 to 12](https://stackoverflow.com/q/32435949/1366033)


| Allowed values | Regex                     |
| -------------- | ------------------------- |
| 0-59           | [1-5]?[0-9]               |
| 0-23           | 2[0-3]|1[0-9]|[0-9]       |
| 1-31           | 3[01]|[12][0-9]|[1-9]     |
| 1-12           | 1[0-2]|[1-9]              |
| 0-6            | [0-6]                     |
| 1970–2099      | 19[7-9][0-9]|20[0-9][0-9] |



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

"anyOf": [
  {
    "properties": { "type": { "const": "icmp" } },
    "required": ["hosts"]
  },
  {
    "properties": {
      "controlType": {"const": "title"}
    },
    "required": ["controlType"]
  },
  {
    "properties": {
      "controlType": {"const": "button"}
    },
    "required": ["controlType"]
  }
],
```

```js
"allOf": [
  {
    "if": {
      "properties": { "type": { "const": "icmp" } }
    },
    "then": {
      "properties": {
        "hosts": {"$ref": "#/definitions/hosts"},
        "wait": {"$ref": "#/definitions/wait"}
      }
    }
  },
  {
    "if": {
      "properties": { "type": { "const": "tcp" } }
    },
    "then": {
      "properties": {
          "postal_code": { "pattern": "[A-Z][0-9][A-Z] [0-9][A-Z][0-9]" }
      }
    }
  },
  {
    "if": {
      "properties": { "type": { "const": "http" } }
    },
    "then": {
      "properties": {
          "postal_code": { "pattern": "[0-9]{4} [A-Z]{2}" } 
      }
    }
  }
],
```


```json
"oneOf": [

  { 
    "properties": {
      "type": { "const": "icmp" },
      "hosts": {"$ref": "#/definitions/hosts"},
      "wait": {"$ref": "#/definitions/wait"}
    }
  },
  { 
    "properties": {
      "type": { "const": "tcp" },
      "hosts": {"$ref": "#/definitions/hosts"}
    }
  },
  { 
    "properties": {
      "type": { "const": "http" },
      "urls": {"$ref": "#/definitions/urls"}
    }
  }
],
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


[Annotate Enum Values with description](https://github.com/json-schema-org/json-schema-spec/issues/57#issuecomment-247861695)

Instead of:

```js
"enum": ["foo", "bar", "whatever"]
```

Do This:

```js
"oneOf": [
    {"const": "foo", "title": "Pick Foo"},
    {"const": "bar", "title": "Pick Bar"},
    {"const": "whatever", "title": "Don't Care"}
]
```

[Make sure item property in array is unique in Json Schema?](https://stackoverflow.com/q/24763759/1366033)

> Nope
