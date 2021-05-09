# Errors

<aside class="notice">
On success call you will get always 200 code.
</aside>

The Global Automotives Cloud API uses the following error codes:


Error Code | Meaning
---------- | -------
206 | No Result -- Based on your request we cannot find the record in our registration database.
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
404 | Not Found -- The specified endpoint or query param could not be found.
406 | Not enough credit -- You have not enough credit to call.
422 | Invalid entity -- Your provided data is not correct format.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Maintenance Mode -- We're upgrading the system, will be back soon.
512 | Internal pricing error. Please contact us, if this error persists.
513 | Internal registration database has been disconnected. Please contact us, if such error persists.

