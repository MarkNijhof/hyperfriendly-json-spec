hyperfriendly-json-spec
==================

A friendly JSON hypermedia format

media-type: "vnd/hyperfriendly+json"

```
{
	"_links" : {
		"self" : { "href" : "..." },
		"templated" : { "href" : ".../{foo}" },
		"form" : { "href" : "", "schema" : { } }
	},
	"_items" : [
		{
			"_links" : {
				"self" : {"href" : "..."}, 
				"next" : {"href" : "..."}, 
				"prev" : {"href" : "..."}
			}
		}
	],
	"_errors" : [
		{
			"title" : "...",
			"message" : "...",
			"code" : "..."
		}
	]
}
```
