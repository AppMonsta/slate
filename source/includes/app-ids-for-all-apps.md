# **App IDs for all apps**

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compressed -u "{API_KEY}:X" "https://api.appmonsta.com/v1/stores/android/ids"
```

```ruby
require 'net/https'
require 'json'

# Request Parameters
store = "android"       # Could be either "android" or "itunes".

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your API own key.
password = "X"          # Password can be anything.

# Request URL
uri = URI("https://api.appmonsta.com/v1/stores/#{store}/ids")

# Ruby Main Code Sample
Net::HTTP.start(uri.host, uri.port,
  :use_ssl => uri.scheme == 'https') do |http|
  request = Net::HTTP::Get.new uri
  request.basic_auth username, password

  http.request request do |response|
      response.read_body do |chunk|
        # Print one app ID per line
        begin
          chunk.each_line do |line|
          print line
          end
        rescue JSON::ParserError
        end
    end
  end
end
```

```python
# This example uses Python Requests library http://docs.python-requests.org/en/master/
import requests
import json

# Request Parameters
store = "android"       # Could be either "android" or "itunes".

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your API own key.
password = "X"          # Password can be anything.

# Request URL
url = 'https://api.appmonsta.com/v1/stores/%s/ids' % store

# This header turns on compression to reduce the bandwidth usage and transfer time.
headers = {'Accept-Encoding': 'deflate, gzip'}

# Python Main Code Sample
response = requests.get(url,
                        auth=(username, password),
                        headers=headers,
                        stream=True)

print response.status_code
for line in response.iter_lines():
  # Print one app ID per line
  print line
```

```java
// This example uses java Unirest library http://unirest.io/java.html

// Request Parameters
store = "android";      // Could be either "android" or "itunes".

// Auth Parameters
username = "{API_KEY}"; // Replace {API_KEY} with your own API key.
password = "X";         // Password can be anything.

// Request URL
requestUrl = "https://api.appmonsta.com/v1/stores/" + store + "android/ids"

// Java Main Code Sample
HttpResponse response = Unirest.get(requestUrl)
  // This header turns on compression to reduce the bandwidth usage and transfer time.
  .header("Accept-Encoding", "deflate, gzip")
  .basicAuth(username, password)
  .asString();

int status = response.getStatus();

BufferedReader in = new BufferedReader(new InputStreamReader(response.getRawBody()));
String line = null;
while((line = in.readLine()) != null) {
  System.out.println(line);
}
```

```php
<?php
// Request Parameters
$store = "android";      // Could be either "android" or "itunes".

// Auth Parameters
$username = "{API_KEY}"; // Replace {API_KEY} with your own API key.
$password = "X";         // Password can be anything.

// Request URL
$url = "https://api.appmonsta.com/v1/stores/$store/ids";

// PHP Main Code Sample
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,$url);
curl_setopt($ch, CURLOPT_USERPWD, $username . ":" . $password);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, 500);
curl_setopt($ch, CURLOPT_WRITEFUNCTION, function($curl, $data) {
    // Print one app ID per line
    echo ($data);
    return strlen($data);
});
curl_exec($ch);
curl_close($ch);
?>
```

> The above code outputs one app ID per line:

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
Get a list of all the app IDs AppMonsta knows about.

### HTTPS Request

`GET https://api.appmonsta.com/v1/stores/<store>/ids`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`.

### Response Fields

One app ID per line.

### Response Headers

Header            | Description
----------------- | -----------
**X-Request-ID**  | The ID of the request to validate via [Request Status API](#get-request-status).

<aside class="notice">
This is a bulk API call. Bulk API calls return one record per line.
</aside>
