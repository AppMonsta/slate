# **App availability**

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compressed -u "{API_KEY}:X" "https://api.appmonsta.com/v1/stores/android/availability.json"
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
uri = URI("https://api.appmonsta.com/v1/stores/#{store}/availability.json")

# Ruby Main Code Sample
Net::HTTP.start(uri.host, uri.port,
  :use_ssl => uri.scheme == 'https') do |http|
  request = Net::HTTP::Get.new uri
  request.basic_auth username, password

  http.request request do |response|
      response.read_body do |chunk|
        # Load json object and print it out
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

# Request Parameters
store = "android"       # Could be either "android" or "itunes".

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your API own key.
password = "X"          # Password can be anything.

# Request URL
request_url = 'https://api.appmonsta.com/v1/stores/%s/availability.json' % store

# This header turns on compression to reduce the bandwidth usage and transfer time.
headers = {'Accept-Encoding': 'deflate, gzip'}

# Python Main Code Sample
response = requests.get(request_url,
                        auth=(username, password),
                        params=req_params,
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

// Request Parameters
store = "android";      // Could be either "android" or "itunes".

// Auth Parameters
username = "{API_KEY}"; // Replace {API_KEY} with your own API key.
password = "X";         // Password can be anything.

// Request URL
requestUrl = "https://api.appmonsta.com/v1/stores/" + store + "android/availability.json"

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
$url = "https://api.appmonsta.com/v1/stores/$store/availability.json";

// PHP Main Code Sample
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,$url);
curl_setopt($ch, CURLOPT_USERPWD, $username . ":" . $password);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, 500);
curl_setopt($ch, CURLOPT_WRITEFUNCTION, function($curl, $data) {
    // Load json object and print it out
    $json_record = json_decode((string)$data, true);
    echo json_encode($json_record);
    return strlen($data);
});
curl_exec($ch);
curl_close($ch);
?>
```

> The above code loads one JSON per line and prints it out:

```
{"app_id":"com.wikia.singlewikia.dragonvale","countries":["FR","DE","JP","US"]}
{"app_id":"com.BLI.CrossTheRoad","countries":["FR","JP","US"]}
{"app_id":"com.singlecase.app","countries":["FR","DE","JP","US"]}
```
Get a list of all the countries where the app is available. The following countries are supported:

`AO`, `AI`, `AL`, `AE`, `AR`, `AM`, `AG`, `AU`, `AT`, `AZ`, `BE`,
`BJ`, `BF`, `BG`, `BH`, `BS`, `BY`, `BZ`, `BM`, `BO`, `BR`, `BB`,
`BN`, `BT`, `BW`, `CA`, `CH`, `CL`, `CN`, `CG`, `CO`, `CV`, `CR`,
`KY`, `CY`, `CZ`, `DE`, `DM`, `DK`, `DO`, `DZ`, `EC`, `EG`, `ES`,
`EE`, `FI`, `FJ`, `FR`, `FM`, `GB`, `GH`, `GM`, `GW`, `GR`, `GD`,
`GT`, `GY`, `HK`, `HN`, `HR`, `HU`, `ID`, `IN`, `IE`, `IS`, `IL`,
`IT`, `JM`, `JO`, `JP`, `KZ`, `KE`, `KG`, `KH`, `KN`, `KR`, `KW`,
`LA`, `LB`, `LR`, `LC`, `LK`, `LT`, `LU`, `LV`, `MO`, `MD`, `MG`,
`MX`, `MK`, `ML`, `MT`, `MN`, `MZ`, `MR`, `MS`, `MU`, `MW`, `MY`,
`NA`, `NE`, `NG`, `NI`, `NL`, `NO`, `NP`, `NZ`, `OM`, `PK`, `PA`,
`PE`, `PH`, `PW`, `PG`, `PL`, `PT`, `PY`, `QA`, `RO`, `RU`, `SA`,
`SN`, `SG`, `SB`, `SL`, `SV`, `ST`, `SR`, `SK`, `SI`, `SE`, `SZ`,
`SC`, `TC`, `TD`, `TH`, `TJ`, `TM`, `TT`, `TN`, `TR`, `TW`, `TZ`,
`UG`, `UA`, `UY`, `US`, `UZ`, `VC`, `VE`, `VG`, `VN`, `YE`, `ZA`,
`ZW`

### HTTPS Request

`GET https://api.appmonsta.com/v1/stores/<store>/availability.json`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`.

### Response Fields

Parameter         | Description 
----------------- | ---------------------
**app_id**        | The app ID of the app.
**countries**     | List of country codes where the app is available.

### Response Headers

Header            | Description
----------------- | -----------
**X-Request-ID**  | The ID of the request to validate via [Request Status API](#get-request-status).

<aside class="notice">
The above code loads one JSON per line and prints it out:
</aside>
