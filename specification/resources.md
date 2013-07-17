#Resources

The resources section of your API spec describes each different type of object that your API will deal with. Your resources section might look like this:

    "resources": {
        "comment": {
            "text": "StringField",
            "_post_id": "ObjectId",
            "email": "EmailField",
            "parent_id": "StringField",
            "post_id": "ObjectId"
        },
        "post": {
            "text": "StringField",
            "email": "EmailField",
            "title": "StringField"
        }
    }


