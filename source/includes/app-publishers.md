# **App publishers**

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compressed -u "{API_KEY}:X" "https://api.appmonsta.com/v1/stores/android/publishers.json?date={{ date }}"
```

```ruby
require 'net/https'
require 'json'

# Request Parameters
store = "android"       # Could be either "android" or "itunes".
date = "{{ date }}"     # Date to check app details against (YYYY-MM-DD).

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your API own key.
password = "X"          # Password can be anything.

# Request URL
uri = URI("https://api.appmonsta.com/v1/stores/#{store}/publishers.json?date=#{date}")

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
date = "{{ date }}"     # Date in YYYY-MM-DD format.

req_params = {"date": date}

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your API own key.
password = "X"          # Password can be anything.

# Request URL
url = 'https://api.appmonsta.com/v1/stores/%s/publishers.json' % store

# This header turns on compression to reduce the bandwidth usage and transfer time.
headers = {'Accept-Encoding': 'deflate, gzip'}

# Python Main Code Sample
response = requests.get(url,
                        auth=(username, password),
                        params=req_params,
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
date = "{{ date }}";    // Date in YYYY-MM-DD format.

// Auth Parameters
username = "{API_KEY}"; // Replace {API_KEY} with your own API key.
password = "X";         // Password can be anything.

// Request URL
requestUrl = "https://api.appmonsta.com/v1/stores/" + store + "android/publishers.json"

// Java Main Code Sample
HttpResponse response = Unirest.get(requestUrl)
  // This header turns on compression to reduce the bandwidth usage and transfer time.
  .header("Accept-Encoding", "deflate, gzip")
  .basicAuth(username, password)
  .queryString("date", date),
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
$date = "{{ date }}";    // Date in YYYY-MM-DD format.

// Auth Parameters
$username = "{API_KEY}"; // Replace {API_KEY} with your own API key.
$password = "X";         // Password can be anything.

// Request URL
$url = "https://api.appmonsta.com/v1/stores/$store/publishers.json?date=$date";

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

> The above code loads one JSON per line and prints it out:

```
{"name":"andavis","url":"http:\/\/www.andavis.de","id":"andavis","address":"","email":"apps@andavis.de"}
{"name":"Air Cab Ltd","url":"http:\/\/aircab.vn","id":"Air Cab Ltd","address":"","email":"aircab.vn@gmail.com"}
{"name":"Right Pulse Works","url":"","id":"Right Pulse Works","address":"","email":"rightpulseapps@gmail.com"}
```
Get a list of all publishers and their information that AppMonsta knows about.

### HTTPS Request

`GET https://api.appmonsta.com/v1/stores/<store>/publishers.json?date=<date>`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`.
**date**          | Yes      |	In the following format: YYYY-MM-DD.

### Response Fields

Parameter         | Description 
----------------- | ---------------------
**name**          | The display name of the publisher.
**id**            | The ID of the publisher as assigned by the store.
**url**           | The website of the publisher.
**address**       | Physical address of the publisher if listed in the app store. ![android_only](../images/android_logo.jpg)
**email**         | The email address of the publisher of this app, if present. ![android_only](../images/android_logo.jpg)

### Response Headers

Header            | Description
----------------- | -----------
**X-Request-ID**  | The ID of the request to validate via [Request Status API](#get-request-status).

<aside class="notice">
The above code loads one JSON per line and prints it out:
</aside>
