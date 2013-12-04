#OPTIONS

The OPTIONS method is used to get information about an end-point.  The OPTIONS method might return some information like this:

    {
      "api": "example-api",
      "methods": [
        "GET",
        "DELETE",
        "PUT",
        "POST"
      ],
      "nav": null,
      "resource": {
        "aliases": {
          "index": true,
          "type": "List"
        },
        "text": "String",
        "title": "String"
      },
      "resource_count": 3
    }

There are a few different sections in the object:

**api** &mdash; the name of the api

**nav** &mdash; options for deeper navigation into child collections

**resource** &mdash; a prototype of the Resource model used in this collection

**resource_count** &mdash; the number of resources in the collection
