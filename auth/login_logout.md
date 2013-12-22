# Login & Logout

MaaSive.net provides a built in auth system to get you up and running quickly.  This section covers how to login & logout of your MaaSive.net API.

The following examples use the [maasivepy][] sdk, available on Github.  Set it up like this:

    from maasivepy import maasivepy
    m = maasivepy.MaaSiveAPISession(
        'https://api.maasive.net/v2/52957bacc3034e4a0fe22f78',
        verbose=True
    )

## Login

To login to your API do this:

    m.login('your_admin_email@maasive.net', 'your_admin_password')

Upon success you will get a response like this:

    LOGIN - https://api.maasive.net/v2/52957bacc3034e4a0fe22f78/auth/login/ in 340.662 ms
    {
      "_created_by": null,
      "_created_ts": null,
      "_email_account_id": null,
      "_super_user": null,
      "_updated_by": null,
      "_updated_ts": null,
      "_version": 0,
      "aliases": [],
      "api": "example-api",
      "email": "example-api@maasive.net",
      "id": "52957ce3c3034e4a0fe22f91",
      "message": "Login Success",
      "password": "<hidden>",
      "permissions": [],
      "roles": [
        "admin"
      ],
      "status": "success",
      "tags": [],
      "token": "auth_token_will_be_here",
      "user": "example-api@maasive.net"
    }

This would be equivalent to the following POST:

    m.post('/auth/login/', data=json.dumps({"email": "your_admin_email@maasive.net", "password": "your_admin_password"}))

## Logout

To logout of your API do this:

    m.get('/auth/logout/')



[maasivepy]: https://github.com/ntrepid8/maasivepy
