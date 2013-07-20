#Concepts

MaaSive.net is designed to help developers and business people build and deploy large, scaleable RESTful APIs.  If you wanted to build a blog this means making it easy to deploy an API with several endpoints like this:

    /my-blog/blog-posts/
    /my-blog/blog-posts/<post_id>
    /my-blog/blog-posts/<post_id>/comments/
    /my-blog/blog-posts/<post_id>/comments/<comment_id>

With MaaSive.net you can deploy an API to provide these endpoints in about 10 minutes!  Below you'll find a helpful overview of the tools that MaaSive.net provides to make it easy to deploy your API.

###API

Each API you design in MaaSive.net is represented by an API Object.  The API Object contains the configuration information that describe to MaaSive what sort of information your API should have, and how it should work.  A basic API might look like this:

    {
        "conf":{
            "debug": true,
            "googleAnalytics": "UA-xxxxxxxx-x",
            "cors": true,
            "files": true,
            "convention": "camelCase"
        },
        "collections":{},
        "resources":{}
    }

The API object serves as a container for the rest of the objects in the API, and for the general configuration data.  The **"conf"** object for our API contains general information about how the entire API should behave.  

The **"debug"** flag set to **true** tells the API to provide a debug endpoint at:

    /my-blog/debug/
    
You can view your recent **Requests** and MaaSive.net's **Responses** at this endpoint and this information should be useful in case you are debugging your application.

The **"googleAnalytics"** key is for the [Google Analytics](http://www.google.com/analytics/) [Web Property ID](https://support.google.com/analytics/answer/1008015?hl=en&ref_topic=1727146).  MaaSive.net will use your code to post analytics information to your account automatically! *(on every endpoint in your API, including files!)*

[Cross-origin Resource Sharing](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing) or CORS provides the ability for web applications hosted on another domain *(e.g. www.foo.com)* to make direct Requests to your API on the api.maasive.net domain.  Browsers don't normally allow web apps to make Cross-origin Requests unless the server supports CORS.  If you want to make direct calls from a browser app, make sure **"cors"** is set to **true** in your **"conf"** object.

But what about file uploads?  Dealing with static files can be a real headache, especially on a web app that needs to scale.  Don't worry, just set your **"files"** key to **true** and let MaaSive.net handle the rest!

Last, but certainly not least, the **"convention"** key tells MaaSive.net which naming convention you want your API to use.  The choices right now are **camelCase** and **underscore**, with underscore being the default.  If you choose **underscore** your keys will look like this:

    "google_analytics"
    
But if you choose **camelCase** your keys will look like this:

    "googleAnalytics"
    
If your API will be primarily consumed by JavaScript applications you probably want to use **camelCase**, but if you hack in Python you probably want **underscore**.  Don't worry though you can change it on a per Request basis so your client apps can all get what they need.

*To learn more about designing your APIs visit: [API Specification](#/docs/specification/api-spec)*

###Resources

Resources are the most fundamental object inside the MaaSive ecosystem.  A Resource is simply an Object that may or may not have a schema associated with it.  Each API owns a set of resources, each representing one type of data.  It is important to remember that Resources have a Model and instances of that model.  When you see a Resource referred to with a capitalized first letter like Resource, we are referring to the Model.  When you see a Resource referred to with a small first letter like resource, we are referring to one or more instances.  A Resource Model defined on an API might look like this:

    {
        "conf":{},
        "collections":{},
        "resources":{
            "BlogPost":{
                "title": "String",
                "text": "String"
            }
        }
    }

*To learn more about designing your Resources visit: [Resource Specification](#/docs/specification/resources)*

###Collections

Collections are views of Resources.  A Collection specifies which subset of resources should be made available, the access controls, and the URL that they should be made available at.  Each API owns a set of Collections, each defining a set or subset of Resource instances that are accessible through that URL.  Collections on an API might look like this:

    {
        "conf":{},
        "collections":{
            "blog-posts":{
                "methods":{
                    "GET":{"requireAuth": false}
                }
            }
        },
        "resources":{
            "BlogPost":{
                "title": "String",
                "text": "String"
            }
        }
    }

*To learn more about designing your Collections visit: [Collection Specification](#/docs/specification/collections)*

