# **Add a new app**

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl -i -s -u "{API_KEY}:X" \
     "https://api.appmonsta.com/v1/stores/android/details/com.rovio.json" -X PUT

HTTP/1.1 202 ACCEPTED
Date: Thu, 26 Sep 2013 22:18:38 GMT
Server: Apache/2.2.20 (Ubuntu)
Set-Cookie: client_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx; expires=Fri, 26-Sep-2014 22:18:38 GMT; Path=/
Vary: Accept-Encoding
Content-Length: 0
Content-Type: text/html; charset=utf-8
```

Tell us about an app we don't know about yet.
We do our best to find all apps, but occasionally we miss one (there isn't a complete list for Google Play).

### HTTPS Request

`PUT https://api.appmonsta.com/v1/stores/<store>/details/<app_id>.json`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`.
**app_id**        | Yes      | The ID of the app to add, e.g. `com.rovio.angrybirds`.

### Response Code
`202` if successfully added.

<aside class="notice">
Newly added app will be available in the next day's dataset.
</aside>
