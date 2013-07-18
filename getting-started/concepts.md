#Concepts

MaaSive.net is designed to help developers and business people build and deploy large, scaleable RESTful APIs.  If you haven't used MaaSive before, or you are new to the concept of a REST API, it would be worth it to read over the material below.

###API

Each API you design in MaaSive.net is represented by an API Object.  The API Object contains the configuration information that describe to MaaSive what sort of information your API should have, and how it should work.

###Resources

Resources are the most fundamental object inside the MaaSive ecosystem.  A Resource is simply an Object that may or may not have a schema associated with it.  Each API owns a set of resources, each representing one type of data.  It is important to remember that Resources have a Model and instances of that model.  When you see a Resource referred to with a capitalized first letter like Resource, we are referring to the Model.  When you see a Resource referred to with a small first letter like resource, we are referring to one or more instances.

###Collections

Collections are views of Resources.  A Collection specifies which subset of resources should be made available, the access controls, and the URL that they should be made available at.  Each API owns a set of Collections, each defining a set or subset of Resource instances that are accessible through that URL.
