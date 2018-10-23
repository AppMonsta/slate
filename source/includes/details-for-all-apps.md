# Details for all apps

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compress -u '{API_KEY}:X' \
    https://api.appmonsta.com/v1/stores/android/details.json?date=2018-10-01&country=US
```

```ruby
require 'net/https'
require 'json'

uri = URI('https://api.appmonsta.com/v1/stores/android/details.json?date=2018-10-01&country=US')
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

payload = {
  "date": "2018-10-01",
  "country": "US",
}

# This header turns on compression to reduce the bandwidth usage and transfer time.
headers = {'Accept-Encoding': 'deflate, gzip'}
response = requests.get("https://api.appmonsta.com/v1/stores/android/details.json?date=2018-10-01&country=US",
                        auth=("{API_KEY}", "X"),
                        params=payload,
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

```php
<?php
$url = "https://api.appmonsta.com/v1/stores/android/details.json?country=US&date=2018-10-12";
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
      "com.axis.mobile",
      "com.creditonebank.mobile",
      "org.westpac.bank",
      "hr.asseco.android.jimba.mUCI.bg",
      "com.bgeneral",
      "com.snapwork.hdfc",
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
  "description": "Shopping, on vacation, or from the comfort of your home – get instant and secure access to your accounts, deposit cheques, pay bills and transfer money with the Churchbridge Credit Union mobile app.<br>Features:<br>•\tView your account activity and recent transactions<br>•\tManage multiple accounts<br>•\tPay bills now or set up payments for the future<br>•\tScheduled payments – view and edit upcoming bills and transfers<br>•\tUse INTERAC® e-Transfer to send money securely via email or text<br>•\tChoose to display your balances onscreen without having to log in<br>•\tGet messages about your account straight to your phone<br>Our mobile app uses the same high level of security as our online banking.  You log into the app in the same way as you would sign into Member Direct and once you log out or close the app your secure session will end.<br>To take advantage of the full functionality of this app, you must already be registered and have logged into Member Direct.  If you wish to enroll for Member Direct online banking please contact us at 1-877-890-2797.<br>There is no charge for the app but mobile data downloading and Internet charges may apply.  Check with your mobile phone provider for details.<br>When you install the app, it will ask for permission to access the following functions of your device:<br>Approximate Location or Precise Location – uses your phone’s GPS to help you find the nearest Branch or ATM.  This can be turned off after the app installation by turning off the phone’s GPS.<br>Take pictures or videos – allows the app to use your camera for the Deposit Anywhere feature in order for you to take pictures of and deposit cheques remotely.<br>Full network access – used to connect to the Internet to allow you to do your mobile banking.<br>View network connection – allows the app to select the best connectivity to operate the app by viewing the types of Internet connectivity available to the Android phone when the mobile banking app is being used.<br>For our privacy and security policy visit, https://churchbridgecu.ca/privacy-policy<br>Visit our website at www.churchbridgecu.ca",
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
    "full network access",
    "take pictures and videos",
    "receive data from Internet",
    "uninstall shortcuts",
    "read your contacts",
    "modify or delete the contents of your USB storage",
    "read the contents of your USB storage",
    "read phone status and identity",
    "precise location (GPS and network-based)",
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


Requesting datasets older than one month:

* We archive all app details datasets which are older than 30 days.
* Historical (older than 30 days) all app details datasets are available only for Monday dates.
* In order to retrieve all apps details for all apps for an older date you will need to first request data for the nearest Monday date and after that fetch and apply only changed app details (by using `only_changed=1` parameter) up to the date you're interested in.

Requesting datasets older than February 2014:

* We archive all app details datasets which are older than February 2014.
* Historical (older than February 2014) all app details datasets are available only for Monday dates.
* We can restore and make available any app details dataset within 2012-2014 on request.


### Response Fields

See previous call, [Details for a single app](#details-for-a-single-app).

### Response Headers

Header            | Description
----------------- | -----------
**X-Request-ID**  | The ID of the request to validate via Request Status API.

<aside class="notice">
Any subscription for API access to this call includes ALL, regardless of what other
countries are included in the subscription.
</aside>
