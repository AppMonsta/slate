# Details for all apps

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compress -u '{API_KEY}:X' \
    https://api.appmonsta.com/v1/stores/android/details.json?date={{ date }}&country=US
```

```ruby
require 'net/https'
require 'json'

date = "{{ date }}"
country = "US"
username = "{API_KEY}"
password = "X" # Password can be anything.

uri = URI('https://api.appmonsta.com/v1/stores/android/details.json?date=#{date}&country=#{country}')

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

params = {
  "date": "{{ date }}",
  "country": "US",
}

# This header turns on compression to reduce the bandwidth usage and transfer time.
headers = {'Accept-Encoding': 'deflate, gzip'}
response = requests.get("https://api.appmonsta.com/v1/stores/android/details.json",
                        auth=("{API_KEY}", "X"),
                        params=params,
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

HttpResponse response = Unirest.get("https://api.appmonsta.com/v1/stores/android/details.json")
  // This header turns on compression to reduce the bandwidth usage and transfer time.
  .header("Accept-Encoding", "deflate, gzip")
  .basicAuth("{API_KEY}", "X")
  .queryString("date", "{{ date }}")
  .queryString("country", "US")
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

$country = "US";
$date = "{{ date }}";
$username = "{API_KEY}";
$password = "X"; // Password can be anything

$url = "https://api.appmonsta.com/v1/stores/android/details.json?country=$country&date=$date";

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

> The above code loads one app record per line and prints them out:

```json
{
  "content_rating": "Everyone",
  "app_name": "Churchbridge Credit Union",
  "top_developer": false,
  "requires_os": "4.4 and up",
  "related": {
    "related_apps": [
      "com.grppl.android.shell.halifax",
      "com.bbva.compassBuzz",
      "com.popular.android.mibanco",
      "nz.co.kiwibank.mobile",
    ],
    "more_from_developer": []
  },
  "video_urls": [],
  "iap_price_range": "",
  "publisher_name": "Churchbridge Credit Union",
  "id": "md.classic.sk.churchbridge.mobileapp",
  "price_currency": "USD",
  "genres": [
    "Finance"
  ],
  "app_type": "APPLICATION",
  "icon_url": "https://lh3.googleusercontent.com/K-Dvu373lxa1c4KjfZO1reaFmNguzMs7CMDRK-jpUXeXXRfHUjNK2Te275KFrcBnIw",
  "content_rating_info": "",
  "interactive_elements": "",
  "version": "13.5.1",
  "publisher_url": "http://www.churchbridgecu.ca",
  "whats_new": "Lock'N'Block",
  "publisher_id": "Churchbridge Credit Union",
  "price": "Free",
  "screenshot_urls": [
    "https://lh3.googleusercontent.com/IUBvJbfBd6jwkWvoq2RCqBcMkGd2UUt9DNihJDTw8X-Flcxmdhy9Ol5uuaQueAM9JgY",
    "https://lh3.googleusercontent.com/BAfxyHOFru8mwP8FdviOQNymqqztb9NNH9kB_-qqqn7DhStJ_N-wqStYqc4n5Zx3tg"
  ],
  "status": "updated",
  "publisher_email": "info@churchbridgecu.ca",
  "description": "Shopping, on vacation, or from the comfort of your home – get instant and secure access to your accounts, ...",
  "price_value": 0,
  "all_rating": 5,
  "store_url": "https://play.google.com/store/apps/details?id=md.classic.sk.churchbridge.mobileapp",
  "downloads": "100+",
  "publisher_address": "",
  "status_unix_timestamp": 1529367053,
  "genre": "Finance",
  "bundle_id": "md.classic.sk.churchbridge.mobileapp",
  "genre_ids": [
    "FINANCE"
  ],
  "all_histogram": {
    "1": 0,
    "3": 0,
    "2": 0,
    "5": 7,
    "4": 0
  },
  "release_date": "2016-03-09",
  "all_rating_count": 7,
  "permissions": [
    "prevent device from sleeping",
    "install shortcuts",
    "view network connections",
    "approximate location (network-based)"
  ],
  "status_date": "June 19, 2018",
  "genre_id": "FINANCE"
}
```
Request the most recent app details for all apps.

### HTTPS Request

`GET https://api.appmonsta.com/v1/stores/<store>/details.json?country=<country_code>&date=<date>`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`.
**country_code**  | Yes      | The two letter country code of the country to fetch app details for, or `ALL` to fetch details for every app, regardless of country.
**date**          | Yes      | In the following format: `YYYY-MM-DD`.
**show_dead**     | No       | If `show_dead=1` is present, show apps that aren't currently available in the store.
**only_changed**  | No       | If `only_changed=1` is present, only show apps that have changed (in any field) since the previous date.

<aside class="notice">
Any subscription for API access to this call includes ALL, regardless of what other
countries are included in the subscription.
</aside>

<aside class="notice">
Requesting datasets older than one month:
<ul>
 <li>We archive all app details datasets which are older than 30 days.</li>
 <li>Historical (older than 30 days) all app details datasets are available only for Monday dates.</li>
 <li>In order to retrieve all apps details for all apps for an older date you will need to first request data for the nearest Monday date and after that fetch and apply only changed app details (by using only_changed=1 parameter) up to the date you're interested in.</li>
</ul>
</aside>

<aside class="notice">
Requesting datasets older than February 2014:
<ul>
 <li> We archive all app details datasets which are older than February 2014.</li>
 <li> Historical (older than February 2014) all app details datasets are available only for Monday dates.</li>
 <li> We can restore and make available any app details dataset within 2012-2014 on request.</li>
</ul>
</aside>


### Response Fields

See previous call, [Details for a single app](#details-for-a-single-app).

### Response Headers

Header            | Description
----------------- | -----------
**X-Request-ID**  | The ID of the request to validate via [Request Status API](#get-request-status).

