# Bond / Swagger (OpenAPI) Attribute Sample
This sample shows a snippet of Bond IDL which expresses data annotations converted to
a sample OpenAPI document. The OpenAPI document is then validated against both JSON
Draft 4 schema and OpenAPI 2.0 schema.

## (Bond Sample IDL)[./sample/bond/sample.bond]
Bond IDL expressing a data annotation.
```
namespace Examples

struct QoSEventPartC
{
    [DataClass("EII")]
    10: required string UserEmailAddress;
    20: optional string UserPUID;
};
```

## (OpenAPI Sample)[./sample/swagger/sample.json]
Swagger document specifying both an endpoint as well as the data schema for QoSEventPartC. See the JSON schema excerpt below:
```json
...
"definitions": {
        "QoSEventPartC": {
            "type": "object",
            "required": [
                "UserEmailAddress"
            ],
            "properties": {
                "UserEmailAddress": {
                    "type": "string",
                    "format": "email",
                    "x-ms-attributes": [
                        "Microsoft.Azure.DataClass.EII"
                    ]
                },
                "UserPUID": {
                    "type": "string"
                }
            }
        }
    }
```

## (JSON Payload Representing the Schema Above)[./sample/example-payload.json]
Sample JSON document which represents the JSON schema above which corresponds to the Bond IDL
```json
{
  "UserEmailAddress": "blah@foo.com",
  "UserPUID":  "foo"
}
```