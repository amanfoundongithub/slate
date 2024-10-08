# Error Description

<aside class="notice">
The Subtl API uses the following error codes for all the requests:
</aside>

Error Code | Meaning
---------- | -------
200 | OK -- The resource was found. 
201 | OK -- The resource was successfully created.
204 | OK -- The resource was deleted successfully. 
400 | Bad Request -- A bad request indicates that you have sent an invalid request format.
404 | Not Found -- The requested resource is not found. 
405 | Method Not Allowed -- The HTTP is not allowed for the request.
422 | Validation Error -- The request could not be validated, possibly due to lack of authentication details.
500 | Internal Server Error -- There is a internal server error, possibly due to some unhandled exception.
503 | Service Unavailable -- The server is temporarily down due to maintenance. 

> In error, the following JSON is returned:

```json
{
  "detail": [
    {
      "loc": [
        "string",
        0
      ],
      "msg": "string",
      "type": "string"
    }
  ]
}
```
