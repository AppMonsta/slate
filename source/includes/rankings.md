# Rankings

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compress -u '{API_KEY}:X' \
    https://api.appmonsta.com/v1/stores/android/rankings.json?date=2018-10-01&country=US
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
response = requests.get("https://api.appmonsta.com/v1/stores/android/rankings.json",
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

HttpResponse response = Unirest.get("https://api.appmonsta.com/v1/stores/android/rankings.json")
  // This header turns on compression to reduce the bandwidth usage and transfer time.
  .header("Accept-Encoding", "deflate, gzip")
  .basicAuth("33dffb8c575ec13c7bc670c82fc5db9e2ff6b72f", "X")
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
response = auth.get('https://api.appmonsta.com/v1/stores/android/rankings.json',
                    :headers => headers,
                    :params => params)

puts response.status

body = response.body
begin
  data = body.readpartial
  puts data
end while data != nil
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

Request all rankings by date and by country.

### HTTPS Request

`GET https://api.appmonsta.com/v1/stores/<store>/rankings.json?country=<country_code>&date=<date>`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`
**country_code**  | Yes      | The two letter country code of any country you've subscribed to.
                  |          | E.g.: `US`, `DE`, `AU`, `FR`, `GB`, `HK`, etc.
**date**          | Yes      | In the following format: `YYYY-MM-DD`.

### Response Fields

Field               | Description
------------------- | -----------
**app_id**          | The app id of the app.
**app_name**        | The name of the app.
**avg_rating**      | An average of the individual ratings, based on a 1-5 scale.
**country**         | The country this ranking list is for; 2 letter country code.
**icon_url**        | The url of the app icon.
**price**           | The price of the app, if it can be scraped from the ranking list.
**publisher_id**    | The id of the publisher of this app as assigned by the store.
**publisher_name**  | The display name of the publisher of this app.
**rank**            | The numerical rank of this app in the given ranking list. Ie, the first app in the list would have 1 for this field, second app would have 2, etc.
**rank_list**       | The identifier of which ranking list this is for. We try and use whatever identifier the store uses when possible. If not, we use the display name of the ranking list from the store.
**timestamp**       | Date/hour when ranking was last updated.

### Response Headers

Header            | Description
----------------- | -----------
**X-Request-ID**  | The ID of the request to validate via Request Status API.

<aside class="notice">
Note This is a bulk API call. Bulk API calls return one record per line.
</aside>
