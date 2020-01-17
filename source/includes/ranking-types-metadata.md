# Ranking types metadata

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compressed -u "{API_KEY}:X" \
     "https://api.appmonsta.com/v1/stores/<store>/rankings/types.json?date={{ date }}"
```

```ruby
require 'net/https'
require 'json'

# Request Parameters
store = "android"       # Could be either "android" or "itunes".
date = "{{ date }}"     # Date in YYYY-MM-DD format.

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your API own key.
password = "X"          # Password can be anything.

# Request URL
uri = URI("https://api.appmonsta.com/v1/stores/#{store}/rankings/types.json?date=#{date}")

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
date = "{{ date }}"     # Date in YYYY-MM-DD format.

req_params = {"date": date}

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your own API key.
password = "X"          # Password can be anything.

# Request URL
request_url = "https://api.appmonsta.com/v1/stores/%s/rankings/types.json" % store

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
date = "{{ date }}";    // Date in YYYY-MM-DD format.

// Auth Parameters
username = "{API_KEY}"; // Replace {API_KEY} with your own API key.
password = "X";         // Password can be anything.

// Request URL
requestUrl = "https://api.appmonsta.com/v1/stores/" + store + "/rankings/types.json";

// Java Main Code Sample
HttpResponse response = Unirest.get(requestUrl)
  // This header turns on compression to reduce the bandwidth usage and transfer time.
  .header("Accept-Encoding", "deflate, gzip")
  .basicAuth(username, password)  
  .queryString("country", $countryCode),
  .queryString("date", $date),
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
$url = "https://api.appmonsta.com/v1/stores/$store/rankings/types.json?date=$date";

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

```json
{"rank_id":"topfreeapplications","name":"Top Free"}
{"rank_id":"newapplications","name":"New Applications"}
{"rank_id":"newgameswelove","name":"New Games We Love RSS"}
```

Request all ranking list types metadata by date.

### HTTPS Request

`GET https://api.appmonsta.com/v1/stores/<store>/rankings/types.json?date=<date>`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`.
**date**          | Yes      | In the following format: `YYYY-MM-DD`.

### Response Fields

Field               | Description
------------------- | -----------
**rank _id**        | Rank ID of an app present in rankings.
**name**            | The name of the app.

### Response Headers

Header            | Description
----------------- | -----------
**X-Request-ID**  | The ID of the request to validate via [Request Status API](#get-request-status).

<aside class="notice">
This is a bulk API call. Bulk API calls return one record per line.
</aside>
