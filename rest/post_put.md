#POST & PUT

In a REST API, the POST method is used for creating new resources in a collection and the PUT method is used for creating or updating a specific resource in a collection.  We made a design decision for MaaSive.net APIs that POST and PUT would both function as an UPSERT.

If an Id is included in the URL or in the object, an update is performed if the resource already exists and a new resource is created if it does not already exist.  If no Id is included in the URL or in the object, a new resource is created.

We made this design choice because some older browsers don't support PUT well, especially with [CORS][].  By treating both POST and PUT as an upsert, we don't break any existing code and make it easy for clients that don't support PUT well to operate just like those that do.

The following examples use the [maasivepy][] sdk, available on Github.  Set it up like this:

    import maasivepy
    m = maasivepy.MaaSiveAPISession(
        'https://api.maasive.net/v2/52957bacc3034e4a0fe22f78',
        verbose=True
    )

## Creating a new Resource

MaaSive.net accepts standard [application/x-www-form-urlencoded][form-encoded] or [application/json][json-encoded] data.  Most Collections require Authentication and Authorization before allowing write privileges, so these examples assume any auth requirements have already been completed.

    m.post(
        '/comments/',
        data=json.dumps({
            "title": "a new comment",
            "text": "this is a brand new comment"
        })
    )

If your request is completed successfully you will get this response body:

    {
      "existing": false,
      "id": "529e83eac3034e4a0fe2d7da",
      "status": "success"
    }

A GET request on the collection with the id from the POST response:

    m.get('/comments/529e83e5c3034e4a0fe2d7d8')

returns this response body:

    {
      "_parent": null,
      "_ts": 1386120165,
      "_version": 1,
      "aliases": [],
      "id": "529e83e5c3034e4a0fe2d7d8",
      "tags": [],
      "text": "this is a brand new comment",
      "title": "a new comment"
    }

## Updating an existing resource

Continuing with the example from above, you may realize that you want to update the text of your comment, and you might do it this way:

    m.put(
        '/comments/529e83e5c3034e4a0fe2d7d8',
        data=json.dumps({
            "text": "updated with a PUT"
        })
    )

and a subsequent GET:

    m.get('/comments/529e83e5c3034e4a0fe2d7d8')

yields this response body:

    {
      "_parent": null,
      "_ts": 1386120165,
      "_version": 2,
      "aliases": [],
      "id": "529e83e5c3034e4a0fe2d7d8",
      "tags": [],
      "text": "updated with a PUT",
      "title": "a new comment"
    }

Because MaaSive.net treats POSTs and PUTs the same as UPSERTS, there are a few more ways you could update the document.  These alternatives may be useful depending on which client you are accessing the API from.

### Id in the Request Body

You can do a PUT with the Id in the request body instead of the URL:

    m.put(
        '/comments/',
        data=json.dumps({
            "id": "529e83e5c3034e4a0fe2d7d8",
            "text": "updated with a PUT and id in the request body"
        })
    )

and a subsequent GET:

    m.get('/comments/529e83e5c3034e4a0fe2d7d8')

yields this response body:

    {
      "_parent": null,
      "_ts": 1386120165,
      "_version": 3,
      "aliases": [],
      "id": "529e83e5c3034e4a0fe2d7d8",
      "tags": [],
      "text": "updated with a PUT and id in the request body",
      "title": "a new comment"
    }

### Update with POST instead of PUT

You don't have to use PUT for update.  You can use POST if you need to like this:

    m.post(
        '/comments/',
        data=json.dumps({
            "id": "529e83e5c3034e4a0fe2d7d8",
            "text": "updated with a POST and id in the request body"
        })
    )

and a subsequent GET:

    m.get('/comments/529e83e5c3034e4a0fe2d7d8')

yields this response body:

    {
      "_parent": null,
      "_ts": 1386120165,
      "_version": 4,
      "aliases": [],
      "id": "529e83e5c3034e4a0fe2d7d8",
      "tags": [],
      "text": "updated with a POST and id in the request body",
      "title": "a new comment"
    }

##Batching Operations

You don't need to create an individual request for each resource you want to create/update.  Each request counts against your quota, and puts additional load on the system so economizing the number of requests by batching helps you and us.

Create two new resources like this:

    m.post(
        '/comments/',
        data=json.dumps([
            {
                "title": "Batch Resource 1",
                "text": "created in a batch"
            },
            {
                "title": "Batch Resource 2",
                "text": "created in a batch"
            }
        ])
    )

If successful it yields a response like this:

    [
      {
        "existing": false,
        "id": "529e8bb01f8eb82279ea9a29",
        "status": "success"
      },
      {
        "existing": false,
        "id": "529e8bb01f8eb82279ea9a2a",
        "status": "success"
      }
    ]

You can verify that the resources look correct with GETs on their Ids:

    m.get('/comments/529e8bb01f8eb82279ea9a29')

gives this response body:

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

and

    m.get('/comments/529e8bb01f8eb82279ea9a2a')

yields this response body:

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

[CORS]: http://en.wikipedia.org/wiki/Cross-origin_resource_sharing
[maasivepy]: https://github.com/ntrepid8/maasivepy
[form-encoded]: http://en.wikipedia.org/wiki/Application/x-www-form-urlencoded#The_application.2Fx-www-form-urlencoded_type
[json-encoded]: http://en.wikipedia.org/wiki/JSON#MIME_type
