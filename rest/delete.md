#DELETE

The DELETE method is exactly what it sounds like.  It deletes resources from collections.  DELETE is like GET in some ways because you can operate on individual resources or you can operate on groups of resources based on a query.

The following examples use the [maasivepy][] sdk, available on Github.  Set it up like this:

    import maasivepy
    m = maasivepy.MaaSiveAPISession(
        'https://api.maasive.net/v2/52957bacc3034e4a0fe22f78',
        verbose=True
    )

## Delete a specific resource

Delete a specific resource like this:

    m.delete('/comments/529e8bb01f8eb82279ea9a29')

which returns this response body:

    {
      "id": "529e8bb01f8eb82279ea9a29",
      "status": "success"
    }

You can verify that the resource was deleted by trying to GET it:

    m.get('/comments/529e8bb01f8eb82279ea9a29')

which returns a 404 error and this response body:

    {
      "error": {
        "extended_code": null,
        "reason": "resource not found",
        "status_code": 404
      }
    }

## Delete a set of resources based on a query:

You can query for a group of resources with DELETE just like you can with GET.  Let's try to query based on a Tag like this:

    m.get('/comments/batch2/')

which returns these two resources in the response body:

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

We can delete them like this:

    m.delete('/comments/batch2/')

which returns this response body:

    [
      {
        "id": "529e96be1f8eb82279ee332d",
        "method": "DELETE",
        "status": "success"
      },
      {
        "id": "529e96be1f8eb82279ee332c",
        "method": "DELETE",
        "status": "success"
      }
    ]

You can check to make sure these are really deleted the same way we did in the example above.  You can also use any of the query methods that work with GET.  You can think of DELETE just like GET except that instead of returning the resources, it deletes them.

[maasivepy]: https://github.com/ntrepid8/maasivepy
