# **Details for a single app**

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compressed -u "{API_KEY}:X" \
     "https://api.appmonsta.com/v1/stores/android/details/com.facebook.orca.json?country=US"
```

```ruby
require 'net/https'
require 'json'

# Request Parameters
store = "android"       # Could be either "android" or "itunes".
country_code = "US"     # Two letter country code.
app_id = "com.facebook.orca" # Unique app identifier (bundle ID).

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your API own key.
password = "X"          # Password can be anything.

# Request URL
uri = URI("https://api.appmonsta.com/v1/stores/#{store}/details/#{app_id}.json?country=#{country_code}")

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
app_id = "com.facebook.orca" # Unique app identifier (bundle ID).

req_params = {"country": country_code}

# Auth Parameters
username = "{API_KEY}"  # Replace {API_KEY} with your own API key.
password = "X"          # Password can be anything.

# Request URL
request_url = "https://api.appmonsta.com/v1/stores/%s/details/%s.json" % (store, app_id)

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
appId = "com.facebook.orca";    // Unique app identifier (bundle ID).

// Auth Parameters
username = "{API_KEY}"; // Replace {API_KEY} with your own API key.
password = "X";         // Password can be anything.

// Request URL
requestUrl = "https://api.appmonsta.com/v1/stores/" + store + "/details/" + appId + ".json"

// Java Main Code Sample
HttpResponse response = Unirest.get(requestUrl)
  // This header turns on compression to reduce the bandwidth usage and transfer time.
  .header("Accept-Encoding", "deflate, gzip")
  .basicAuth(username, password)
  .queryString("country", countryCode)
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
$appId = "com.facebook.orca";    // Unique app identifier (bundle ID).

// Auth Parameters
$username = "{API_KEY}"; // Replace {API_KEY} with your own API key.
$password = "X";         // Password can be anything.

// Request URL
$url = "https://api.appmonsta.com/v1/stores/$store/details/$appId.json?country=US";

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

> The above code loads one app record and prints it out:

```json
{
  "content_rating": "Everyone",
  "app_name": "Messenger – Text and Video Chat for Free",
  "top_developer": false,
  "publisher_id_num": "5629993546372213086",
  "requires_os": "Varies with device",
  "related": {
    "related_apps": [
      "com.soundcloud.android",
      "com.spotify.music",
      "com.facebook.workchat",
      ...,
      "com.facebook.lite",
      "com.whatsapp",
      "com.viber.voip"
    ],
    "more_from_developer": [
      "com.facebook.katana",
      "com.facebook.mlite",
      ...,
      "com.facebook.study",
      "com.facebook.viewpoints"
    ]
  },
  "video_urls": [],
  "file_size": "Varies with device",
  "publisher_name": "Facebook",
  "id": "com.facebook.orca",
  "price_currency": "USD",
  "genres": [
    "Communication"
  ],
  "app_type": "APPLICATION",
  "icon_url": "https://lh3.googleusercontent.com/rkBi-WHAI-dzkAIYjGBSMUToUoi6SWKoy9Fu7QybFb6KVOJweb51NNzokTtjod__MzA",
  "content_rating_info": "",
  "interactive_elements": "Users Interact, Shares Location, Digital Purchases",
  "version": "Varies with device",
  "publisher_url": "https://www.facebook.com/games/fbmessenger_android/",
  "contains_ads": false,
  "whats_new": "In efforts to make it easier to connect with businesses on Messenger, we are focusing on more contextual...",
  "publisher_id": "Facebook",
  "price": "Free",
  "screenshot_urls": [
    "https://lh3.googleusercontent.com/AG0QK9DwMCnhIMxBzqmCvB8T7YINdg6HzhInEoW5r72f2KaKhJ63TLwnb0GYNrOMICc",
    ...,
    "https://lh3.googleusercontent.com/f-d7nreVZFtpS7d1Fxc6n2RjYeCN1DzXsorep0iv0thslN0akBNk4ATma5FFPK1jnzaQ"
  ],
  "status": "updated",
  "publisher_email": "android-support@fb.com",
  "description": "Be together whenever with a simple way to text, video chat and rally the group...",
  "price_value": 0,
  "all_rating": 4.2,
  "store_url": "https://play.google.com/store/apps/details?id=com.facebook.orca",
  "downloads": "1,000,000,000+",
  "publisher_address": "1 Hacker Way\nMenlo Park, CA 94025",
  "status_unix_timestamp": 1578526140,
  "genre": "Communication",
  "privacy_url": "https://m.facebook.com/policy.php",
  "editors_choice": true,
  "genre_ids": [
    "COMMUNICATION"
  ],
  "iap_price_range": "$0.99 - $399.99 per item",
  "all_histogram": {
    "1": 7649347,
    "3": 4624657,
    "2": 2246616,
    "5": 48309851,
    "4": 7605518
  },
  "release_date": "2014-01-30",
  "all_rating_count": 70435991,
  "bundle_id": "com.facebook.orca",
  "permissions": [
    "receive text messages (SMS)",
    "change your audio settings",
    ...,
    "control Near Field Communication",
    "read the contents of your USB storage",
    "control vibration"
  ],
  "status_date": "January 8, 2020",
  "genre_id": "COMMUNICATION"
}

```

Request the most recent app details with the app's unique ID.

### HTTPS Request

`GET https://api.appmonsta.com/v1/stores/<store>/details/<app_id>.json?country=<country_code>`

### Request Parameters

Parameter         | Required | Value
----------------- | -------- | -----------
**store**         | Yes      | `android` or `itunes`.
**country_code**  | Yes      | The two letter country code of the country to fetch this app's details for, or `ALL` if you don't care which country.
**app_id**        | Yes      | The unique app identifier (bundle ID) for the correct store.
**show_dead**     | No       | If `show_dead=1` is present, show apps that aren't currently available in the store.

<aside class="notice">
Any subscription for API access to this call includes ALL, regardless of what other
countries are included in the subscription.
</aside>

### Response Fields

Field                    | Description
------------------------ | -----------
**all_histogram**        | The histogram breakdown of ratings for all versions of this app. A dictionary with the keys 1-5 (as strings) mapped onto number of reviews with that number of stars.
**all_rating**           | The average rating for all versions of this app.
**all_rating_count**     | The number of ratings for all versions of this app.
**all_reviews**          | The number of reviews for all versions of this app, if available as a summarized number. ![itunes_only](../images/itunes_logo.jpg)
**app_name**             | The name of the app.
**app_type**             | Whether the app is categorized as `GAME` or `APPLICATION`. ![android_only](../images/android_logo.jpg)
**bundle_id**            | The internal bundle identifier of the app binary.
**contains_ads**         | Whether the app is marked on the store as containing ads or not. ![android_only](../images/android_logo.jpg)
**content_rating**       | The age-appropriate content rating of the app.
**content_rating_info**  | Additional info on content rating of the app if present. ![android_only](../images/android_logo.jpg)
**current_histogram**    | The histogram breakdown of ratings for the current version of this app. Should be a dictionary with the keys 1-5 (as strings) mapped onto number of reviews with that number of stars. ![itunes_only](../images/itunes_logo.jpg)
**current_rating**       | The average rating for the current version of this app. ![itunes_only](../images/itunes_logo.jpg)
**current_rating_count** | The number of ratings for the current version of this app. ![itunes_only](../images/itunes_logo.jpg)
**current_reviews**      | The number of reviews for the current version of this app, if available as a summarized number. ![itunes_only](../images/itunes_logo.jpg)
**description**          | The text of the description of the app.
**downloads**            | The number of downloads this app has, if available. ![android_only](../images/android_logo.jpg)
**editors_choice**       | Whether the app is marked on the store as an editor's choice or not. ![android_only](../images/android_logo.jpg)
**file_size**            | The file size of the downloadable app as a human readable string, if present. Value is displayed as shown in each store.
**file_size_bytes**      | The size of the app binary in bytes, if present. ![itunes_only](../images/itunes_logo.jpg)
**genre**                | The primary category of an app, as it appears on the store side.
**genre_id**             | The ID of the primary category of an app, as returned by the store.
**genres**               | All categories of an app, as they are returned from the store side.
**genre_ids**            | List of category IDs of an app, as returned by the store.
**has_game_center**      | A boolean (0 or 1) indicating whether this app supports Game Center. ![itunes_only](../images/itunes_logo.jpg)
**iap_price_range**      | Price range of all in-app products available for the app. ![android_only](../images/android_logo.jpg)
**icon_url**             | The url of the app icon.
**id**                   | The unique identifier for the app as assigned by the store.
**in_app_purchases**     | In the iTunes store a list containing all available in-app products. ![itunes_only](../images/itunes_logo.jpg)

```json--inline
"in_app_purchases": [
  {
    "rank": "1",
    "name": "Town Folk - Skin Pack",
    "price": "$0.99"
  },
  {
    "rank": "2",
    "name": "City Folk - Skin Pack",
    "price": "$0.99"
  }
],
```
 &nbsp;                  | &nbsp;
------------------------ | ------
**interactive_elements** | A string containing interactive elements as listed on the app page. ![android_only](../images/android_logo.jpg)
**is_universal**         | Whether the app is universal, meaning it's optimized for both iPhone and iPad. ![itunes_only](../images/itunes_logo.jpg)
**languages**            | Languages that the app supports, as they're defined on the store side. ![itunes_only](../images/itunes_logo.jpg)
**permissions**          | List of permissions required by this app. ![android_only](../images/android_logo.jpg)

```json--inline
"permissions": [
  "prevent device from sleeping",
  "view network connections",
  "find accounts on the device",
  "full network access",
  "receive data from Internet",
  "access extra location provider commands",
  "read phone status and identity",
  "precise location (GPS and network-based)",
  "approximate location (network-based)"
]
```
 &nbsp;                   | &nbsp;
------------------------  | ------
**price**                 | The price of the app, as displayed on the store side.
**price_currency**        | Price currency, according to ISO 4271 standard.
**price_value**           | Price value, expressed as digits only.
**privacy_url**           | Privacy policy URL provided by the publisher, if present. ![android_only](../images/android_logo.jpg)
**publisher_address**     | Physical address of the publisher if listed in the app store. ![android_only](../images/android_logo.jpg)
**publisher_email**       | The email address of the publisher of this app, if present. ![android_only](../images/android_logo.jpg)
**publisher_id**          | The ID of the publisher of this app as assigned by the store.
**publisher_id_num**      | The numeric ID of the publisher of this app as assigned by the store. ![android_only](../images/android_logo.jpg)
**publisher_name**        | The display name of the publisher of this app.
**publisher_url**         | The website of the publisher of this app.
**related**               | A dictionary of related apps as presented by the source system. The keys are an identifier for the section of related apps, such as `also_installed`. The values are lists of app IDs.
**release_date**          | String containing app release date in ISO format.
**requires_hardware**     | A string indicating which hardware is required to run this app. ![itunes_only](../images/itunes_logo.jpg)
**requires_os**           | A string indicating the minimum OS/platform version this app requires, if present.
**screenshot_urls**       | An array of screenshot urls.
**seller**                | App seller name as it appears on Apple’s App Store. ![itunes_only](../images/itunes_logo.jpg)
**status**                | Indicates an app status, in relationship to its <code>status_date</code>. If it is either "updated" or "released", the app is available for download. If it is "dead", the app is no longer present in the store.
**status_date**           | The date the app was updated or released, as a string in whatever format it's displayed on the store.
**status_unix_timestamp** | The parsed unix timestamp of the `status_date` field.
**store_url**             | App store URL.
**support_url**           | A support url for this app, if it differs from `publisher_url`. ![itunes_only](../images/itunes_logo.jpg)
**translated_description**| Translated app description, when in other language than expected. ![android_only](../images/android_logo.jpg)
**version**               | The current version of the app.
**video_urls**            | An array of urls of demo videos for this app, if present. ![android_only](../images/android_logo.jpg)
**whats_new**             | The text of the "What's new in this version" writeup, if present.

