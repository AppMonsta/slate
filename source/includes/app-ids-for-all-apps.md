# App IDs for all apps

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compress -u '{API_KEY}:X' https://api.appmonsta.com/v1/stores/android/ids
```

```python
# This example uses Python Requests library http://docs.python-requests.org/en/master/
import requests

payload = {
}

# This header turns on compression to reduce the bandwidth usage and transfer time.
headers = {'Accept-Encoding': 'deflate, gzip'}
response = requests.get("https://api.appmonsta.com/v1/stores/android/ids",
                        auth=("{API_KEY}", "X"),
                        params=payload,
                        headers=headers,
                        stream=True)

print response.status_code
for app_id in response.iter_lines():
  print app_id
```

```java
// This example uses java Unirest library http://unirest.io/java.html

HttpResponse response = Unirest.get("https://api.appmonsta.com/v1/stores/android/ids")
  // This header turns on compression to reduce the bandwidth usage and transfer time.
  .header("Accept-Encoding", "deflate, gzip")
  .basicAuth("{API_KEY}", "X")
  .queryString("apiKey", "123")
  .asString();

int status = response.getStatus();

BufferedReader in = new BufferedReader(new InputStreamReader(response.getRawBody()));
String appId = null;
while((appId = in.readLine()) != null) {
  System.out.println(appId);
}
```
```ruby
# This example uses http Ruby gem https://github.com/httprb/http
require 'http'

params = {
}

# This header turns on compression to reduce the bandwidth usage and transfer time.
headers =  {'Accept-Encoding' => "deflate, gzip" }
auth = HTTP.basic_auth(:user => '{API_KEY}', :pass => 'X')
response = auth.get('https://api.appmonsta.com/v1/stores/android/ids',
                    :headers => headers,
                    :params => params)

puts response.status

body = response.body
begin
  app_id = body.readpartial
  puts app_id
end while app_id != nil
```

> The above code loads one record per line and prints it out:

```
air.com.escapegamesmobi.CuckooBirdRescue
air.elisashopingdressupgames
appinventor.ai_antonello_f_caterino.PoLet500
appinventor.ai_nyanskyaw.Alpha_SVM
ar.com.hermesonline.autoya
ar3plus.siudase.baju
bigdx.adw.slick.purple
biz.buildapps.ahucabs
cm.williamsofttech.gallerylockphotoandvideohideapplock
co.vpsoft.kiribati_newspapers
```
Get a list of all the app ids AppMonsta knows about

### HTTPS Request

`GET https://api.appmonsta.com/v1/stores/<store>/ids`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`

### Response Fields

One app ID per line.

### Response Headers

Header            | Description
----------------- | -----------
**X-Request-ID**  | The ID of the request to validate via Request Status API.

<aside class="notice">
NOTE: This is a bulk API call. Bulk API calls return one record per line.
</aside>
