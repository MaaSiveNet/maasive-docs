# Registration

MaaSive.net provides a built in user registration system so you can get up and running quickly.

The following examples use the [maasivepy][] sdk, available on Github.  Set it up like this:

    from maasivepy import maasivepy
    m = maasivepy.MaaSiveAPISession(
        'https://api.maasive.net/v2/52957bacc3034e4a0fe22f78',
        verbose=True
    )

## Register a new user

To register a new user do this:

    m.post('/auth/register/', data=json.dumps({"email": "josh@maasive.net", "password": "asdf1234"}))

Upon success this will trigger a welcome email if you have that configured in your API settings.  You can also automatically assign users roles when they register.
