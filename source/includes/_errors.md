# Errors

The Co-Life API uses the following error codes:


Error Code | Meaning
---------- | -------
401 | Unauthorized -- Your authentication token is missing or don't grant you access for this.
404 | Not Found -- You tried to reach a resource that isn't available for you.
422 | Unprocessable entity -- There are issues with the body of your request.

Further explanation about why the error is happening is given in the body of the HTTP response!
