#hyperfriendly-json-spec

A friendly JSON hypermedia format

**media-type:** "vnd/hyperfriendly+json"

##Example

```javascript
{
  "_links": {
    "self": {
      "href": "/users/page=2"
    },
    "next": {
      "href": "/users?page=3"
    },
    "prev": {
      "href": "/users?page=1"
    },
    "find": {
      "href": "/users/search?name={name}"
    },
    "create": {
      "href": "/users",
      "method": "post",
      "schema": {
        "description": "A user",
        "type": "object",
        "properties": {
          "firstname": {
            "type": "string",
            "title": "First Name"
          },
          "lastname": {
            "type": "string",
            "title": "Last Name"
          }
        }
      }
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
  ],
  "_errors": [
    {
      "title": "Some error",
      "message": "Some error has occurred",
      "code": "XYZ123"
    }
  ]
}
```
