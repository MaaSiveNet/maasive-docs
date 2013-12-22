# Verification

MaaSive.net provides a built in user email verification system so you can verify a user's email address.

The following examples use the [maasivepy][] sdk, available on Github.  Set it up like this:

    from maasivepy import maasivepy
    m = maasivepy.MaaSiveAPISession(
        'https://api.maasive.net/v2/52957bacc3034e4a0fe22f78',
        verbose=True
    )

## Verify a User's email address

MaaSive.net handles user email verification using an optional field on the User Resource.  To get started add this field to your User Resource:

    {"verified": "VerifiedEmail"}

Also, make sure you have configured the email templates in your API settings like this:

    "verify": {
        "verify_email_tpl": {
            "text": "Please verify yoru email by clicking the following link: http://your-site.com/#/verify?token={{ token }}",
            "subject": "Verify your Email"
        },
        "roles": [
            "verified"
        ]
    }

Your handler should then POST the token to your MaaSive.net API like this:

    m.post('/auth/verify/', data=json.dumps({"token": "token_content"})

[maasivepy]: https://github.com/ntrepid8/maasivepy
