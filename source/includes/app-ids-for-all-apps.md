# App IDs for all apps

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compress -u '{API_KEY}:X' \
    https://api.appmonsta.com/v1/stores/android/ids
```

```ruby
require 'net/https'
require 'json'

uri = URI('https://api.appmonsta.com/v1/stores/android/ids')
username = "{API_KEY}"
password = "X" # Password can be anything.

Net::HTTP.start(uri.host, uri.port,
  :use_ssl => uri.scheme == 'https') do |http|
  request = Net::HTTP::Get.new uri
  request.basic_auth username, password

  http.request request do |response|
      response.read_body do |chunk|
        # Parse/load and print valid json data
        begin
          chunk.each_line do |line|
          json_record = JSON.parse(line)
          print json_record
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


# This header turns on compression to reduce the bandwidth usage and transfer time.
headers = {'Accept-Encoding': 'deflate, gzip'}
response = requests.get("https://api.appmonsta.com/v1/stores/android/ids",
                        auth=("{API_KEY}", "X"),
                        headers=headers,
                        stream=True)

print response.status_code
for line in response.iter_lines():
  # Load json object and print it out
  json_record = json.loads(line)
  print json_record
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
String line = null;
while((line = in.readLine()) != null) {
  System.out.println(line);
}
```

```php
<?php
$url = "https://api.appmonsta.com/v1/stores/android/ids";
$username = "{API_KEY}";
$password = "X"; // Password can be anything

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,$url);
curl_setopt($ch, CURLOPT_USERPWD, $username . ":" . $password);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, 500);
curl_setopt($ch, CURLOPT_WRITEFUNCTION, function($curl, $data) {
    // Parse json and print data
    $json_record = json_decode((string)$data, true);
    echo json_encode($json_record);
    return strlen($data);
});
curl_exec($ch);
curl_close($ch);
?>
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
Get a list of all the app ids AppMonsta knows about.

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
NOTE: This is a bulk API call. Bulk API calls return one record per line.
</aside>
