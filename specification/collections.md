#Collections

Collections are the part of an API that provide access to a set (or subset) of resources, at a specific URL, and restrict which users can access that set or subset of resources.  Here is an example of a simple collection:

    {
        "comments": {
            "methods": {
                "get": {
                    "require_auth": true,
                },
                "put": {
                    "require_auth": true,
                },
                "post": {
                    "require_auth": true,
                },
                "delete": {
                    "require_auth": true,
                }
            },
            "query": {},
            "resource": "Comment"
        }
    }

This collection provides access to the entire set of resources of the type Comment.  Four methods, are provided and access is restricted to logged in users.  This is a simple example but it provides the four basic CRUD methods and access control.

## Access Control by Role

To restrict access to a certain role, use **allow_roles** in the method specification like this:

    {
        "comments": {
            "methods": {
                "get": {
                    "require_auth": true,
                    "allow_roles": ["admin", "customer"]
                },
                "put": {
                    "require_auth": true,
                },
                "post": {
                    "require_auth": true,
                },
                "delete": {
                    "require_auth": true,
                }
            },
            "query": {},
            "resource": "Comment"
        }
    }

Different methods can allow different roles:

    {
        "comments": {
            "methods": {
                "get": {
                    "require_auth": true,
                    "allow_roles": ["admin", "customer"]
                },
                "put": {
                    "require_auth": true,
                    "allow_roles": ["admin"]
                },
                "post": {
                    "require_auth": true,
                    "allow_roles": ["admin"]
                },
                "delete": {
                    "require_auth": true,
                    "allow_roles": ["admin"]
                }
            },
            "query": {},
            "resource": "Comment"
        }
    }

## A Subset of Resources

One of the most powerful ways to organize an API is to allow a different level of access to different (but possibly) overlapping subsets of a single Resource type.  For example, an API may require that the comments be tagged with **published** before they can be accessed by users without the **staff** role like this:

    {
        "comments": {
            "methods": {
                "get": {
                    "require_auth": false
                }
            },
            "query": {
                "tags": ["published"]
            },
            "resource": "Comment"
        },
        "staff": {
            "collections": {
                "comments": {
                    "methods": {
                        "get": {
                            "require_auth": true,
                            "allow_roles": ["staff"]
                        },
                        "put": {
                            "require_auth": true,
                            "allow_roles": ["staff"]
                        },
                        "post": {
                            "require_auth": true,
                            "allow_roles": ["staff"]
                        },
                        "delete": {
                            "require_auth": true,
                            "allow_roles": ["staff"]
                        }
                    },
                    "query": {},
                    "resource": "Comment"
                }
            }
        }
    }
