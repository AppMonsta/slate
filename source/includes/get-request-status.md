# **Get Request Status**

Validate a bulk API request to see if it is successfully completed or had any errors.


### HTTPS Request

`https://api.appmonsta.com/v1/request/<request_id>`

### Request Method: GET

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**request_id**    | Yes      | The ID that's sent via X-Request-ID.

### Response Fields

Field                    | Description
------------------------ | -----------
**status**               | Can be SUCCESS, ERROR, or ABORTED, if the request completed successfully, there are server side errors or the client aborted the request, respectively.
**request_id**           | Equals to the request ID given as parameter.
**records**              | Number of records sent as response. Only available on SUCCESS.
**md5**                  | md5 sum of the response data. This does not include headers, but only the HTTP body sent. Only available on SUCCESS.

### Examples

For a successfully completed request:

```json--inline
{
  "status": "SUCCESS",
  "records": 10,
  "md5": "2909acb51bdb441b1f29f703ae6831e2",
  "request_id": "874995c4d75b4cb6bb8bbf6d3ef1d2da"
}
```

For requests that failed because of server error:

```json--inline
{
  "status": "ERROR"
  "request_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

For an aborted request:

```json--inline
{
  "status": "ABORTED"
  "request_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

For an unknown request:

```json--inline
{
"message": "Unknown request id request_id."
}
```

<aside class="warning">
This API will return ERROR for all ongoing requests. Please make sure to query this API after the connection ends.
</aside>
