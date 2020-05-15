# Errors

<aside class="notice">
This error section helps you have a clue of what you are doing wrong
</aside>

The Kovatek API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your Authentication credentials is wrong.
403 | Forbidden -- You don't have enough permision to perform request.
404 | Not Found -- The specified resource could not be found.
405 | Method Not Allowed -- You tried to access an endpoint with an invalid method.
409 | Conflict -- You input isn't unique.
410 | Gone -- The resource requested has been removed from our servers.
418 | I'm a teapot.
429 | Too Many Requests -- You're requesting too many resources! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
