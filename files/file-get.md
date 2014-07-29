# File GET

You can access files with a GET just like you access your JSON documents.  There are a few quirks which we will discuss also.

## File GET from Browser

To make it easy to incorporate files into your API, files can be access directly from the browser:

![file-access.png](https://s3.amazonaws.com/maasive-docs/assets/images/file-access.png)

This is the same file that we uploaded in the file POST example.  Here it is accessed through an `/images/` Collection with the Collection Resource set to `file`.  Other access restrictions can be added if desired.

If desired the files can be listed in the data explorer just like JSON documents are:

![data-image-collection.png](https://s3.amazonaws.com/maasive-docs/assets/images/data-image-collection.png)

## /files/ Collection

An API user with the `admin` role can always access all of the files stored in an API from the `/files/` collection.  This special collection is convenient for administrative tasks, but you must provision a public facing Collection if you want to make files available to your users.

![data-files-service.png](https://s3.amazonaws.com/maasive-docs/assets/images/data-files-service.png)
