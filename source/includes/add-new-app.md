# Add a New App

Tell us about an app we don't know about yet.
We do our best to find all apps, but occasionally we miss one (there isn't a complete list for Google Play).

### HTTPS Request

`https://api.appmonsta.com/v1/stores/<store>/details/<app_id>.json`

### Request Method: PUT

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`.
**app_id**        | Yes      | the id of the app to add, e.g. com.rovio.angrybirds.

### Response: 202 if successfully added


```
$ curl -i -s -u '<your_api_key>:X' https://api.appmonsta.com/v1/stores/android/details/com.rovio.json -X PUT

HTTP/1.1 202 ACCEPTED
Date: Thu, 26 Sep 2013 22:18:38 GMT
Server: Apache/2.2.20 (Ubuntu)
Set-Cookie: client_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx; expires=Fri, 26-Sep-2014 22:18:38 GMT; Path=/
Vary: Accept-Encoding
Content-Length: 0
Content-Type: text/html; charset=utf-8
```
<aside class="notice">
NOTE: The app details will be available within 10 minutes under normal circumstances. 
You can poll (no faster than every 10 seconds) the Details for a Single App method to wait for the app to be available.
</aside>
