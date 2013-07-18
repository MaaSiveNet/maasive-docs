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

If include the **debug** key in your conf section and set its value to *true*, your API will make a "debug collection" available for you at /<api_name>/debug/ where you will find the 10 most recent Requests