# Reviews for all apps

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compress -u '{API_KEY}:X' \
    https://api.appmonsta.com/v1/stores/<store>/reviews.json?language=<language>
```
```python
# This example uses Python Requests library http://docs.python-requests.org/en/master/
import requests
import json

payload = {
  "date": "2018-10-01",
  "country": "US",
}

# This header turns on compression to reduce the bandwidth usage and transfer time.
headers = {'Accept-Encoding': 'deflate, gzip'}
response = requests.get("https://api.appmonsta.com/v1/stores/android/reviews.json",
                        auth=("{API_KEY}", "X"),
                        params=payload,
                        headers=headers,
                        stream=True)

print response.status_code
for line in response.iter_lines():
  record = json.loads(line)
  print record
```
```java
// This example uses java Unirest library http://unirest.io/java.html

HttpResponse response = Unirest.get("https://api.appmonsta.com/v1/stores/android/reviews.json")
  // This header turns on compression to reduce the bandwidth usage and transfer time.
  .header("Accept-Encoding", "deflate, gzip")
  .basicAuth("{API_KEY}", "X")
  .queryString("apiKey", "123")
  .queryString("date", "2018-10-01")
  .queryString("country", "US")
  .asString();

int status = response.getStatus();

BufferedReader in = new BufferedReader(new InputStreamReader(response.getRawBody()));
String line = null;
while((line = in.readLine()) != null) {
  System.out.println(line);
}
```
```ruby
# This example uses http Ruby gem https://github.com/httprb/http
require 'http'

params = {
  :date => "2018-10-01",
  :country => "US",
}

# This header turns on compression to reduce the bandwidth usage and transfer time.
headers =  {'Accept-Encoding' => "deflate, gzip" }
auth = HTTP.basic_auth(:user => '{API_KEY}', :pass => 'X')
response = auth.get('https://api.appmonsta.com/v1/stores/android/reviews.json',
                    :headers => headers,
                    :params => params)

puts response.status

body = response.body
begin
  data = body.readpartial
  puts data
end while data != nil
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
**language**      | Yes      | Specify language with two letter language code (ie, EN, FR, IT, etc).
**start_date**    | Yes      | Only returns reviews we have collected after this date. This can sometimes include few days older records than `start_date`, since it can take some time for us to scrape the reviews. It can also include even older reviews if they have changed in any way since the first time we have collected them.
**end_date**      | No       | Used with `start_date` parameter to get reviews we have collected within a particular time frame. If not specified we default this parameter to current date.

### Response Fields

Field                    | Description
------------------------ | -----------
**app_id**               | The app id of the app this review is for.
**app_version**          | The app version this review is for, if present.
**date**                 | Review date as a string in ISO format: YYYY-MM-DD.
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

