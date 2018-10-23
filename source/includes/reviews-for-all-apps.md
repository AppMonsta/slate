# Reviews for all apps

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compress -u '{API_KEY}:X' \
    https://api.appmonsta.com/v1/stores/android/reviews.json?language=en
```

```ruby
require 'net/https'
require 'json'

uri = URI('https://api.appmonsta.com/v1/stores/android/reviews.json?language=en')
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
response = requests.get("https://api.appmonsta.com/v1/stores/android/reviews.json?language=en",
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

HttpResponse response = Unirest.get("https://api.appmonsta.com/v1/stores/android/reviews.json?language=en")
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
$url = "https://api.appmonsta.com/v1/stores/android/reviews.json?language=en";
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

> The above code returns reviews records in bulk; these will look like below:

```json
{
  "rating":5,
  "user_id":"103142985936483271758",
  "review_id":"Z3A6QU9xcFRPSDNlbTBHR0dTdy1GSkhrWFJjYnl4dThZamhKNm4zTUwtYzBkZW9Ud0owWDBLUDBlRWJZSVFNbUdnbEViNlJRclRCMzZCbXh6eENZUm9hVXc",
  "language":"en",
  "title":"Heartbleed Detector",
  "user_name":"Ken Mosburg",
  "app_id":"com.trendmicro.tool.heartbleeddetector",
  "review_text":"So far so good, fast, Said Weather Channel & Tune-In Radio apps vulnerable.  4 other weather apps not affected?",
  "date":"2014-04-19",
  "date_str":"April 19, 2014"
}
```

Request most recent app reviews dump.
This is a bulk API call, returning one record per line.

### HTTPS Request

`GET https://api.appmonsta.com/v1/stores/<store>/reviews.json?country=<country_code>&date=<date>`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`.
**language**      | Yes      | Specify language with two letter language code (`EN`, `FR`, `IT`, etc.).
**start_date**    | Yes      | Only returns reviews we have collected after this date. This can sometimes include few days older records than `start_date`, since it can take some time for us to scrape the reviews. It can also include even older reviews if they have changed in any way since the first time we have collected them.
**end_date**      | No       | Used with `start_date` parameter to get reviews we have collected within a particular time frame. If not specified we default this parameter to current date.

### Response Fields

Field                    | Description
------------------------ | -----------
**app_id**               | The app id of the app this review is for.
**app_version**          | The app version this review is for, if present.
**date**                 | Review date as a string in ISO format: `YYYY-MM-DD`.
**date_str**             | The original review date format, a string.
**device**               | The device the user is using, if present.
**language**             | The language the review was written in.
**last_scraped**         | Timestamp representing review last scrape date.
**rating**               | The star rating the user gave with this review. 1-5.
**review_id**            | The id assigned by the store. May be non-unique across apps.
**review_text**          | The text of the body of the review.
**title**                | The title/subject line of the review, as written by the user, if there is one.
**user_id**              | The unique identifier for the user as assigned by the store ( deprecated for iTunes ). ![android_only](../images/android_logo.jpg)
**user_name**            | The display name of the user writing the review.

### Response Headers
Header           | Description
---------------- | -----------
**X-Request-ID** | The ID of the request to validate via ![Request Status API](#get-request-status).

