# Details for a single app

> Don't forget to replace `{API_KEY}` with your actual API key.

```shell
curl --compress -u '{API_KEY}:X' \
    https://api.appmonsta.com/v1/stores/android/details/com.facebook.orca.json?country=US
```

```python
# This example uses Python Requests library http://docs.python-requests.org/en/master/
import requests
import json

payload = {
  "country": "US",
}

# This header turns on compression to reduce the bandwidth usage and transfer time.
headers = {'Accept-Encoding': 'deflate, gzip'}
response = requests.get("https://api.appmonsta.com/v1/stores/android/details/com.facebook.orca.json",
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

HttpResponse response = Unirest.get("https://api.appmonsta.com/v1/stores/android/details/com.facebook.orca.json")
  // This header turns on compression to reduce the bandwidth usage and transfer time.
  .header("Accept-Encoding", "deflate, gzip")
  .basicAuth("{API_KEY}", "X")
  .queryString("apiKey", "123")
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
  :country => "US",
}

# This header turns on compression to reduce the bandwidth usage and transfer time.
headers =  {'Accept-Encoding' => "deflate, gzip" }
auth = HTTP.basic_auth(:user => '{API_KEY}', :pass => 'X')
response = auth.get('https://api.appmonsta.com/v1/stores/android/details/com.facebook.orca.json',
                    :headers => headers,
                    :params => params)

puts response.status

body = response.body
begin
  data = body.readpartial
  puts data
end while data != nil
```

> The above code loads one app record and prints it out:

```json
{
  "content_rating": "Everyone",
  "app_name": "Messenger – Text and Video Chat for Free",
  "top_developer": false,
  "requires_os": "Varies with device",
  "related": {
    "related_apps": [
      "com.zing.zalo",
      "com.snapchat.android",
      "com.facebook.talk",
      "com.skype.m2",
      "com.android.chrome",
      "com.truecaller",
      "com.beint.zangi"
    ],
    "more_from_developer": [
      "com.facebook.katana",
      "com.facebook.mlite",
      "com.facebook.lite",
      "com.facebook.talk",
      "com.facebook.Socal",
      "com.facebook.pages.app",
      "com.facebook.moments"
    ]
  },
  "video_urls": [ ],
  "iap_price_range": "$0.99 - $399.99 per item",
  "publisher_name": "Facebook",
  "id": "com.facebook.orca",
  "price_currency": "USD",
  "genres": [
    "Communication"
  ],
  "app_type": "APPLICATION",
  "icon_url": "https://lh5.ggpht.com/0VYAvZLR9YhosF-thqm8xl8EWsCfrEY_uk2og2f59K8IOx5TfPsXjFVwxaHVnUbuEjc",
  "content_rating_info": "",
  "interactive_elements": "Users Interact, Shares Location, Digital Purchases",
  "version": "Varies with device",
  "publisher_url": "https://www.facebook.com/games/fbmessenger_android/",
  "whats_new": "Now you can see your call history and missed calls—all in one place.",
  "publisher_id": "Facebook",
  "price": "Free",
  "screenshot_urls": [
    "https://lh3.googleusercontent.com/Akz7U1QW4I1KKNiig-uum5an_P4JBnKyVPXda5LozfcZUgnG3g2amnLn2Oili42b0wM",
    "https://lh3.googleusercontent.com/mD90pAw4RL6tv5gFmarSsUuPtTqO2WEBagbFGXEw-5qdBzA-giCd5f_wwjQvNF2V0g",
    "https://lh3.googleusercontent.com/ThIwGgGqT-cMX_8nICixYSwN8NRruUr0io4HsUQkOqwjRSw0rcSJdapE-WAomPjaJ34",
    "https://lh3.googleusercontent.com/idgO2Vxw3e107SRc3YM5CE2p0a7B1vaKNnCHx6IIqrTUa_08fXp2Tu8OdHOQmG_KVjB_",
    "https://lh3.googleusercontent.com/L0MHXxoPUJqLY3ANVTATSv26EKDiyN_ZlXLaHWtIo5zKgIySJ7u34BIpEfK9emVpXQ"
  ],
  "status": "updated",
  "publisher_email": "android-support@fb.com",
  "description": "Instantly connect with the people in your life. Messenger is free, fast, and secure. <br><br>- Reach anyone. You can use names or phone numbers to find friends. <br>- Use everywhere. Messenger works across all mobile and desktop devices. You can even connect with people internationally!   <br>- Connect however you want. Send a text message, share a photo, or start a video chat — all in Messenger. <br>- Communicate better with groups. Catch up in real time with high quality group video chat or customize your messaging experience with colors, nicknames, and group photos. <br>- Call and video chat your friends 1:1 or in groups. It's free over Wi-Fi (otherwise standard data charges apply), so talk as long as you want, even with people in other countries. <br>- Express yourself. Send emojis, stickers, and GIFs to conversations or add new masks and effects to your video chats. <br>- Capture photos and videos with fun art and effects. You can save these to camera roll, send to conversations, or post to your Day, a place where people can see what you're up to.  <br>- Play games and compete with your friends. You can compare scores and see how you rank against other people. <br>- Chat with businesses. You can make reservations, check on orders, and get real-time customer service.",
  "price_value": 0,
  "all_rating": 4,
  "store_url": "https://play.google.com/store/apps/details?id=com.facebook.orca",
  "downloads": "1,000,000,000+",
  "publisher_address": "1 Hacker Way\nMenlo Park, CA 94025",
  "status_unix_timestamp": 1538443703,
  "genre": "Communication",
  "bundle_id": "com.facebook.orca",
  "genre_ids": [
    "COMMUNICATION"
  ],
  "all_histogram": {
    "1": 7266140,
    "2": 2320959,
    "3": 5434492,
    "4": 8418707,
    "5": 34682503
  },
  "release_date": "2011-11-07",
  "all_rating_count": 58122801,
  "permissions": [
    "receive text messages (SMS)",
    "change your audio settings",
    "record audio",
    "read your text messages (SMS or MMS)",
    "read calendar events plus confidential information",
    "reroute outgoing calls",
    "read your contacts",
    "send sticky broadcast",
    "take pictures and videos",
  ],
  "status_date": "October 2, 2018",
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
**show_dead**     | No       | If show_dead=1 is present, show apps that aren't currently available in the store.

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
**content_rating**       | The age-appropriate content rating of the app.
**content_rating_info**  | Additional info on content rating of the app if present. ![android_only](../images/android_logo.jpg)
**current_histogram**    | The histogram breakdown of ratings for the current version of this app. Should be a dictionary with the keys 1-5 (as strings) mapped onto number of reviews with that number of stars. ![itunes_only](../images/itunes_logo.jpg)
**current_rating**       | The average rating for the current version of this app. ![itunes_only](../images/itunes_logo.jpg)
**current_rating_count** | The number of ratings for the current version of this app. ![itunes_only](../images/itunes_logo.jpg)
**current_reviews**      | The number of reviews for the current version of this app, if available as a summarized number. ![itunes_only](../images/itunes_logo.jpg)
**description**          | The text of the description of the app.
**downloads**            | The number of downloads this app has, if available. ![android_only](../images/android_logo.jpg)
**file_size**            | The file size of the downloadable app as a human readable string, if present.
**file_size_bytes**      | The size of the app binary in bytes, if present.
**genre**                | The primary category of an app, as it appears on the store side.
**genre_id**             | The id of the primary category of an app, as returned by the store.
**genres**               | All categories of an app, as they are returned from the store side.
**genre_ids**            | List of category ids of an app, as returned by the store.
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
**price**                 | The price of the app.
**publisher_address**     | Physical address of the publisher if listed in the app store. ![android_only](../images/android_logo.jpg)
**publisher_email**       | The email address of the publisher of this app, if present. ![android_only](../images/android_logo.jpg)
**publisher_id**          | The id of the publisher of this app as assigned by the store.
**publisher_name**        | The display name of the publisher of this app.
**publisher_url**         | The website of the publisher of this app. ![android_only](../images/android_logo.jpg)
**related**               | A dictionary of related apps as presented by the source system. The keys are an identifier for the section of related apps, such as `also_installed`. The values are lists of app ids.
**release_date**          | String containing app release date in ISO format.
**requires_hardware**     | A string indicating which hardware is required to run this app. ![itunes_only](../images/itunes_logo.jpg)
**requires_os**           | A string indicating the minimum OS/platform version this app requires, if present.
**screenshot_urls**       | An array of screenshot urls.
**seller**                | App seller name as it appears on Apple’s App Store. ![itunes_only](../images/itunes_logo.jpg)
**status**                | Indicates what `status_date` is in relationship to. If it is either "updated" or "released", the app is available for download. If it is "dead", the app is no longer present in the store.
**status_date**           | The date the app was updated or released, as a string in whatever format it's displayed on the store.
**status_unix_timestamp** | The parsed unix timestamp of the `status_date` field.
**store_url**             | App store URL.
**support_url**           | A support url for this app, if it differs from `publisher_url`. ![itunes_only](../images/itunes_logo.jpg)
**top_developer**         | A boolean whether this apps developer is marked as a top developer. ![android_only](../images/android_logo.jpg)
**version**               | The current version of the app.
**video_urls**            | An array of urls of demo videos for this app, if present.
**whats_new**             | The text of the "What's new in this version" writeup, if present.

<aside class="notice">
Any subscription for API access to this call includes ALL, regardless of what other
countries are included in the subscription.
</aside>
