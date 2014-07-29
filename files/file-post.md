# File POST

To upload files to your API use the HTTP POST method.  You can either use the `application/x-www-form-urlencoded` Content-Type or you can POST the file directly as the body of the request.  Both methods are explained in examples below.

These examples use the maasivepy Python SDK which is available on GitHub:

<https://github.com/MaaSiveNet/maasive-py>

## Direct file POST

If you have a local file on your computer and you want to upload it to your API, you can do this:

    import maasivepy
    example = maasivepy.APISession('https://api.maasive.net/v2.4.2/53adbcdb68fdfb3e5be1a99c', admin_key='<your_admin_key>')
    with open('/Users/ntrepid8/Desktop/bike_jump.jpg', 'rb') as f:
        example.post('/files/', data=f.read(), headers={'Content-Type': 'image/jpeg'})

Now you can see the file in your `/files/` collection:

![uploaded-file.png](https://s3.amazonaws.com/maasive-docs/assets/images/uploaded-file.png)

You can verify this by accessing it with a GET request.  Here is an example of accessing this files in the browser after enabling an `/images/` Collection:

![file-access.png](https://s3.amazonaws.com/maasive-docs/assets/images/file-access.png)

You can see more about the `/images/` collection in the file GET examples.
