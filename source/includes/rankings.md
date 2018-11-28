# **App rankings**

## General rankings
> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compress -u "{API_KEY}:X" \
     "https://api.appmonsta.com/v1/stores/android/rankings.json?date={{ date }}&country=US"
```

```ruby
require 'net/https'
require 'json'

# Request Parameters
store = "android"       # Could be either "android" or "itunes".
country_code = "US"     # Two letter country code.
date = "{{ date }}"     # Date in YYYY-MM-DD format.

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your API own key.
password = "X"          # Password can be anything.

# Request URL
uri = URI("https://api.appmonsta.com/v1/stores/android/rankings.json?date=#{date}&country=#{country_code}")

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
country_code = "US"     # Two letter country code.
date = "{{ date }}"     # Date in YYYY-MM-DD format.

req_params = {"date": date,
              "country": country_code}

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your own API key.
password = "X"          # Password can be anything.

# Request URL
request_url = "https://api.appmonsta.com/v1/stores/%s/rankings.json" % store

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
countryCode = "US";     // Two letter country code.
date = "{{ date }}";    // Date in YYYY-MM-DD format.

// Auth Parameters
username = "{API_KEY}"; // Replace {API_KEY} with your own API key.
password = "X";         // Password can be anything.

// Request URL
requestUrl = "https://api.appmonsta.com/v1/stores/" + store + "/rankings.json";

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
$countryCode = "US";     // Two letter country code.
$date = "{{ date }}";    // Date in YYYY-MM-DD format.

// Auth Parameters
$username = "{API_KEY}"; // Replace {API_KEY} with your own API key.
$password = "X";         // Password can be anything.

// Request URL
$url = "https://api.appmonsta.com/v1/stores/$store/rankings.json?country=$countryCode&date=$date";

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
{
  "rank_list": "apps_movers_shakers-ANDROID_WEAR",
  "app_name": "Robinhood: Invest in Stock, Crypto, ETF & Coin",
  "timestamp": "2018-10-01 17:13:59",
  "country": "US",
  "price": "Free",
  "app_id": "com.robinhood.android",
  "rank": 1,
  "publisher_id": "Robinhood",
  "icon_url": "https://lh3.googleusercontent.com/LvWOyUYOe8xovqUdbIoMCIUnqoW2gInudnwzczSFsCAvP20BqKTFZHWBdTl_j9WdPBPW=w170-rw",
  "publisher_name": "Robinhood",
  "avg_rating": "4.6"
}
{
  "rank_list": "apps_movers_shakers-ANDROID_WEAR",
  "app_name": "Any.do: To-do list, Calendar, Reminders & Planner",
  "timestamp": "2018-10-01 17:13:59",
  "country": "US",
  "price": "Free",
  "app_id": "com.anydo",
  "rank": 2,
  "publisher_id": "Any.do",
  "icon_url": "https://lh3.googleusercontent.com/ZAn8LqhPFlUgBC7s25IHSmwEw6dDAYKOIBA9yCsCk2B6STy5gmzchlh2xyeD_AHd4T4=w170-rw",
  "publisher_name": "Any.do",
  "avg_rating": "4.5"
}
```

Request all rankings by date and by country. This call returns ranking records with all the available meta-data from the ranking list page.

### HTTPS Request

`GET https://api.appmonsta.com/v1/stores/<store>/rankings.json?country=<country_code>&date=<date>`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`.
**country_code**  | Yes      | The two letter country code of any country you've subscribed to.
                  |          | E.g.: `US`, `DE`, `AU`, `FR`, `GB`, `HK`, etc.
**date**          | Yes      | In the following format: `YYYY-MM-DD`.

### Response Fields

Field               | Description
------------------- | -----------
**app_id**          | The app ID of the app.
**app_name**        | The name of the app.
**avg_rating**      | An average of the individual ratings, based on a 1-5 scale. ![android_only](../images/android_logo.jpg)
**country**         | The country this ranking list is for; 2 letter country code.
**icon_url**        | The url of the app icon.
**price**           | The price of the app, if it can be scraped from the ranking list.
**publisher_id**    | The ID of the publisher of this app as assigned by the store.
**publisher_name**  | The display name of the publisher of this app.
**rank**            | The numerical rank of this app in the given ranking list. Ie, the first app in the list would have 1 for this field, second app would have 2, etc.
**rank_list**       | The identifier of which ranking list this is for. We try and use whatever identifier the store uses when possible. If not, we use the display name of the ranking list from the store.
**timestamp**       | Date/hour when ranking was last updated.

### Response Headers

Header            | Description
----------------- | -----------
**X-Request-ID**  | The ID of the request to validate via [Request Status API](#get-request-status).

<aside class="notice">
This is a bulk API call. Bulk API calls return one record per line.
</aside>

## Aggregated rankings

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compress -u "{API_KEY}:X" \
     "https://api.appmonsta.com/v1/stores/android/aggregate.json?date={{ date }}&country=US"
```

```ruby
require 'net/https'
require 'json'

# Request Parameters
store = "android"       # Could be either "android" or "itunes".
country_code = "US"     # Two letter country code.
date = "{{ date }}"     # Date in YYYY-MM-DD format.

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your API own key.
password = "X"          # Password can be anything.

# Request URL
uri = URI("https://api.appmonsta.com/v1/stores/android/aggregate.json?date=#{date}&country=#{country_code}")

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
country_code = "US"     # Two letter country code.
date = "{{ date }}"     # Date in YYYY-MM-DD format.

req_params = {"date": date,
              "country": country_code}

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your own API key.
password = "X"          # Password can be anything.

# Request URL
request_url = "https://api.appmonsta.com/v1/stores/%s/rankings/aggregate.json" % store

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
countryCode = "US";     // Two letter country code.
date = "{{ date }}";    // Date in YYYY-MM-DD format.

// Auth Parameters
username = "{API_KEY}"; // Replace {API_KEY} with your own API key.
password = "X";         // Password can be anything.

// Request URL
requestUrl = "https://api.appmonsta.com/v1/stores/" + store + "/rankings/aggregate.json";

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
$countryCode = "US";     // Two letter country code.
$date = "{{ date }}";    // Date in YYYY-MM-DD format.

// Auth Parameters
$username = "{API_KEY}"; // Replace {API_KEY} with your own API key.
$password = "X";         // Password can be anything.

// Request URL
$url = "https://api.appmonsta.com/v1/stores/$store/rankings/aggregate.json?country=$countryCode&date=$date";

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
{"ranks":["com.free.daily.horoscope.zodiac.secret","com.valpak.android",
          "com.srpinfosoft.Claptoflashlightonoff","com.tuya.smart",...],
 "country":"US",
 "rank_id":"apps_movers_shakers",
 "genre_id":"LIFESTYLE"}

{"ranks":["479516143","763692274","1396301917","640364616",...],
 "country":"US",
 "rank_id":"toppaidapplications",
 "genre_id":"7002"}
```


Request aggregated rankings by date and by country. This call returns records with ranked app ID's per country and per genre/type (not other meta-data). It's ideal if you're only interested in app rank positions.

<aside class="notice">
App ID's in the list are sorted according to their rank (from the top to the bottom). First app in the list is the top ranking app.
</aside>

### HTTPS Request

`GET https://api.appmonsta.com/v1/stores/<store>/rankings/aggregate.json?country=<country_code>&date=<date>`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`.
**country_code**  | Yes      | The two letter country code of any country you've subscribed to.
                  |          | E.g.: `US`, `DE`, `AU`, `FR`, `GB`, `HK`, etc.
**date**          | Yes      | In the following format: `YYYY-MM-DD`.

### Response Fields

Field               | Description
------------------- | -----------
**country**         | The country this ranking list is for; 2 letter country code.
**genre_id**        | String representing rankin list genre/category, as returned by the store. We force “overall” ID value for top level ranking lists.
**rank_id**         | Ranking list type (string), which serves as identifier and it's set by stores.
**ranks**           | A list of ordered app ID's. (array of strings for consistency between iTunes and Google Play stores).

### Response Headers

Header            | Description
----------------- | -----------
**X-Request-ID**  | The ID of the request to validate via [Request Status API](#get-request-status).

<aside class="notice">
This is a bulk API call. Bulk API calls return one record per line.
</aside>

## Genres metadata

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compress -u "{API_KEY}:X" \
     "https://api.appmonsta.com/v1/stores/<store>/rankings/genres.json?date={{ date }}"
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
uri = URI("https://api.appmonsta.com/v1/stores/#{store}/rankings/genres.json?date=#{date}")

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
request_url = "https://api.appmonsta.com/v1/stores/%s/rankings/genres.json" % store

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
requestUrl = "https://api.appmonsta.com/v1/stores/" + store + "/rankings/genres.json";

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
$url = "https://api.appmonsta.com/v1/stores/$store/rankings/genres.json?date=$date";

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
{"name":"Music & Audio","genre_id":"MUSIC_AND_AUDIO"}
{"name":"Auto & Vehicles","genre_id":"AUTO_AND_VEHICLES"}
{"parent_id":"FAMILY","name":"Family Brain Games","genre_id":"FAMILY_BRAINGAMES"}

{"name":"Books","genre_id":"6018"}
{"name":"Stickers","genre_id":"6025"}
{"parent_id":"6021","name":"Health, Mind & Body","genre_id":"13017"}
```

Request all available ranking genres (also known as categories) by date. If you use [aggregated](#aggregated-rankings) API call, then this call will map genre IDs to human readable genre names.

### HTTPS Request

`GET https://api.appmonsta.com/v1/stores/<store>/rankings/genres.json?date=<date>`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`.
**date**          | Yes      | In the following format: `YYYY-MM-DD`.

### Response Fields

Field               | Description
------------------- | -----------
**genre_id**        | Genre ID of an app present in rankings.
**name**            | The name of the app.
**parent_id**       | Parent genre ID (optional).

### Response Headers

Header            | Description
----------------- | -----------
**X-Request-ID**  | The ID of the request to validate via [Request Status API](#get-request-status).

<aside class="notice">
This is a bulk API call. Bulk API calls return one record per line.
</aside>

## List types metadata

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compress -u "{API_KEY}:X" \
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

{"rank_id":"apps_movers_shakers","name":"Trending Apps"}
{"rank_id":"apps_tablet_featured","name":"Staff Picks for Tablet"}
{"rank_id":"apps_topselling_new_free","name":"Top New Free"}
```

Request all ranking types by date. Ranking types are ranking list types (names) as defined by the Google Play or iTunes store. If you use [aggregated](#aggregated) ranks API call, then this call will map ranking types to their human-readable names.

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
