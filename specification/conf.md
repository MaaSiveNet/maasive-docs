#Conf

The **conf** section of the API spec instructs your API how to behave and which services to include in your API.  A typical conf section for an API in the development stage might look like this:

    {
        "debug": true,
        "google_analytics": "UA-42331324-1",
        "convention": "camelCase",
        "files": true,
        "cors": true
    }
    
###debug

If include the **debug** key in your conf section and set its value to *true*, your API will make a "debug collection" available for you at /api_slug/debug/ where you will find the 10 most recent Requests and the Responses that MaaSive sent back.  It might look like this:

    {
        "51e5f64953d4c904e7fee35c": {
            "response": {
                "body": {
                    "51e5f2c953d4c904e7fee2df": {
                        "tags": [],
                        "text": "asdfasdf",
                        "email": "foo@bar.com",
                        "parentid": null,
                        "postid": "51e4c29753d4c904e7fedda5",
                        "id": "51e5f2c953d4c904e7fee2df",
                        "aliases": []
                    },
                    "51e5f62453d4c904e7fee33f": {
                        "tags": [],
                        "text": "asdfasdf",
                        "email": "foo@baz.net",
                        "parentid": null,
                        "postid": "51e4c29753d4c904e7fedda5",
                        "id": "51e5f62453d4c904e7fee33f",
                        "aliases": []
                    }
                },
                "headers": {
                    "content-length": "375",
                    "access-control-allow-methods": "OPTIONS, GET, POST, PUT, DELETE",
                    "server": "TornadoServer/2.4",
                    "etag": "\"b2a7a814b9e896efeb3e6e52084a51b6009196d0\"",
                    "access-control-allow-credentials": "true",
                    "access-control-allow-origin": "http://localhost:9000",
                    "access-control-allow-headers": "x-Custom-Header, X-Requested-With, origin, content-type",
                    "content-type": "application/json; charset=UTF-8"
                }
            },
            "aliases": [],
            "request": {
                "body": {},
                "headers": {
                    "origin": "http://localhost:9000",
                    "accept-language": "en-US,en;q=0.8",
                    "accept-encoding": "gzip,deflate,sdch",
                    "connection": "close",
                    "accept": "application/json, text/plain, */*",
                    "user-agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36",
                    "host": "SuperSpock",
                    "x-requested-with": "XMLHttpRequest",
                    "m-request-uri": "/spencer/posts/51e4c29753d4c904e7fedda5/comments/",
                    "m-release": "SuperSpock",
                    "referer": "http://localhost:9000/"
                },
                "remoteIp": "127.0.0.1",
                "uri": "/spencer/posts/51e4c29753d4c904e7fedda5/comments/",
                "method": "GET"
            },
            "id": "51e5f64953d4c904e7fee35c",
            "tags": []
        }
    }