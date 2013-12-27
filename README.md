#hyperfriendly-json-spec

A friendly JSON hypermedia format

**media-type:** "vnd/hyperfriendly+json"

##Vanilla JSON

hyperfriendly+json is a superset of JSON. The following is therefore valid hyperfriendly+json.

```javascript
{
  "firstName": "Bob",
  "lastName": "Anderson",
  "address": {
    "street": "Somestreet",
    "postalCode": "1337",
    "city": "Leetville"
  }
}
```

##With links

A hyperfriendly+json object MAY contain a _links object. If present, this object MUST contain at least one link. A link MUST contain a href which can be an absolute or a releative uri.

```javascript
{
  "_links": {
    "self": {
      "href": "/users/1"
    },
    "friends": {
      "href": "/friends/1"
    }
  },
  "firstName": "Bob",
  "lastName": "Anderson",
  "address": {
    "street": "Somestreet",
    "postalCode": "1337",
    "city": "Leetville"
  }
}
```

##Templated urls

Links MAY contain templated uris conforming to the spec (http://tools.ietf.org/html/rfc6570)

```javascript
{
  "_links" : {
    "byName": {
      "href": "/users?name={name}"
    }
  }
}
```

##Forms

A link MAY contain a schema element conforming to the json schema spec (http://json-schema.org/)

```javascript
{
  "_links": {
    "create": {
      "href": "/users",
      "method": "POST",
      "schema": {
        "title": "Create user",
        "type": "object",
        "properties": {
          "firstName": {
            "type": "string",
            "required": true
          },
          "lastName": {
            "type": "string",
            "required": true
          },
          "address": {
            "type": "object",
            "properties": {
              "street": {
                "type": "string"
              },
              "postalCode": {
                "type": "integer",
                "minimum": 0,
                "maximum": 9999
              }
            }
          }
        }
      }
    }
  }
}
```

##Forms with external schema

Json schema also supports referencing other schema.

```javascript
{
  "_links": {
    "create": {
      "href": "/users",
      "method": "POST",
      "schema": {
        "$ref": "http://api.test.com/schema/new-user.json"
      }
    }
  }
}
```

##Collections

A resource MAY contain an _items array. When an _items array is present the resource is a collection resource. The collection resource MAY contain a next link and MAY contain a prev link.

```javascript
{
  "_links" : {
    "self": {
      "href": "/users/page=2"
    },
    "next": {
      "href": "/users?page=3"
    },
    "prev": {
      "href": "/users?page=1"
    }
  },
  "_items": [
    {
      "_links": {
        "self": {
          "href": "/users/11"
        }
      }
    },
    {
      "_links": {
        "self": {
          "href": "/users/12"
        }
      }
    }
  ]
}
```

##Errors

A resource MAY contain an _errors collection. A error item MUST have a title and a message.

```javascript
{
  "_errors": [
    {
      "title": "Some error",
      "message": "Some error has occurred"
    }
  ]
}
```
