#GET

The GET method is used to perform "reads" and "queries" on resources in your collections.

The following examples use the [maasivepy][] sdk, available on Github.  Set it up like this:

    import maasivepy
    m = maasivepy.MaaSiveAPISession(
        'https://api.maasive.net/v2/52957bacc3034e4a0fe22f78',
        verbose=True
    )

## Find All

The most general GET is a "find all" where you don't specify any parameters and the API just gives you back all the resources in the collections (up to the limit).  Do a "find all" GET like this:

    m.get('/comments/')

And the response body you get back could look like this:

    [
      {
        "_parent": null,
        "_ts": 1386122160,
        "_version": 1,
        "aliases": [],
        "id": "529e8bb01f8eb82279ea9a2a",
        "tags": [],
        "text": "created in a batch",
        "title": "Batch Resource 2"
      },
      {
        "_parent": null,
        "_ts": 1386122160,
        "_version": 1,
        "aliases": [],
        "id": "529e8bb01f8eb82279ea9a29",
        "tags": [],
        "text": "created in a batch",
        "title": "Batch Resource 1"
      }
    ]

## Find One

If you only want a single resource and you know the Id you can GET it like this:

    m.get('/comments/529e8bb01f8eb82279ea9a2a')

Which yields this response body:

    {
      "_parent": null,
      "_ts": 1386122160,
      "_version": 1,
      "aliases": [],
      "id": "529e8bb01f8eb82279ea9a2a",
      "tags": [],
      "text": "created in a batch",
      "title": "Batch Resource 2"
    }

## Tags

One of the most powerful concepts in MaaSive.net APIs is the concept of Tagging.  Tags are an ad hoc taxonomy system for your resources.  You can use them to slice and dice Collections according to User Roles or Logical Groups or whatever.

Let's say we have a collection of resources that looks like this:

    [
      {
        "_parent": null,
        "_ts": 1386124990,
        "_version": 1,
        "aliases": [],
        "id": "529e96be1f8eb82279ee332d",
        "tags": [
          "batch2"
        ],
        "text": "created in a batch",
        "title": "Batch Resource 4"
      },
      {
        "_parent": null,
        "_ts": 1386124990,
        "_version": 1,
        "aliases": [],
        "id": "529e96be1f8eb82279ee332c",
        "tags": [
          "batch2"
        ],
        "text": "created in a batch",
        "title": "Batch Resource 3"
      },
      {
        "_parent": null,
        "_ts": 1386122160,
        "_version": 1,
        "aliases": [],
        "id": "529e8bb01f8eb82279ea9a2a",
        "tags": [],
        "text": "created in a batch",
        "title": "Batch Resource 2"
      },
      {
        "_parent": null,
        "_ts": 1386122160,
        "_version": 1,
        "aliases": [],
        "id": "529e8bb01f8eb82279ea9a29",
        "tags": [],
        "text": "created in a batch",
        "title": "Batch Resource 1"
      }
    ]

For whatever reason we only want the resources tagged with "batch2".  To get only those resources do this:

    m.get('/comments/batch2/')

which yields the response body:

    [
      {
        "_parent": null,
        "_ts": 1386124990,
        "_version": 1,
        "aliases": [],
        "id": "529e96be1f8eb82279ee332d",
        "tags": [
          "batch2"
        ],
        "text": "created in a batch",
        "title": "Batch Resource 4"
      },
      {
        "_parent": null,
        "_ts": 1386124990,
        "_version": 1,
        "aliases": [],
        "id": "529e96be1f8eb82279ee332c",
        "tags": [
          "batch2"
        ],
        "text": "created in a batch",
        "title": "Batch Resource 3"
      }
    ]

Nice!  But the best part is that Tags are automatically indexed on MaaSive.net's database.  That means that your queries using Tags are much faster than a query that is not indexed.  Tags are not your only option for indexing, you can specify an index on any field you want, but Tags are powerful because they can be created at run time, without requiring any change in your data schema.

## Query Args

You may find that you want to query a collection for resources based on a specific value in a specific field.  You can do that like this:

    m.get('/comments/', params={"title": "Batch Resource 3"})

Just in case its a little confusing not to see the query string in the URI, the very cool [Requests][] library for Python is turning the above code into this URI:

    /comments/?title=Batch+Resource+3

which yields this response body:

    [
      {
        "_parent": null,
        "_ts": 1386124990,
        "_version": 1,
        "aliases": [],
        "id": "529e96be1f8eb82279ee332c",
        "tags": [
          "batch2"
        ],
        "text": "created in a batch",
        "title": "Batch Resource 3"
      }
    ]

[maasivepy]: https://github.com/ntrepid8/maasivepy
[requests]: http://www.python-requests.org
