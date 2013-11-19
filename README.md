#hyperfriendly-json-spec

A friendly JSON hypermedia format

**media-type:** "vnd/hyperfriendly+json"

##Vanilla JSON
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
```javascript
{
  "_links" : {
    "byName": {
      "href": "/users?name={name}"
    }
  }
}
```

##Templated with optional parameters
```javascript
{
  "_links" : {
    "search": {
      "href": "/users?name={name}",
      "optional": {
        "occupation": "&occupation={occupation}",
        "city": "&city={city}"
      }
    }
  }
}
```

##Forms
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
```javascript
{
  "_errors": [
    {
      "title": "Some error",
      "message": "Some error has occurred",
      "code": "XYZ123"
    }
  ]
}
```
