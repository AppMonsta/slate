---
title: AppMonsta API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - java
  - php

toc_footers:
  - <a href='/support'>Contact Support</a>
  - <a href='/dashboard/get_api_key/'>Get My API Key</a>

includes:
  - rankings
  - app-ids-for-all-apps
  - details-for-a-single-app
  - details-for-all-apps
  - reviews-for-all-apps
  - add-new-app
  - get-request-status

search: true
---

# Introduction

AppEverything API gives you access to:

* [Rankings](#rankings): Apps that show up on ranking lists (ie. Overall, Top Grossing, etc).
* [Details](#details-for-a-single-app):  Basic data about each app (data on the app description page). Get data about single app or all apps with one API call.
* [Reviews](#reviews-for-all-apps): User reviews associated with each app.
* And more.

<aside class="notice">
  You need to get an API key before you can use our API. It's free and you can grab it
  <a href="/dashboard/get_api_key/"> here </a>.<br>
  Complete access to this API is available via monthly subscription.
  <a href="/contact-sales"> Contact us </a> for pricing and details or try out limited access
  for free.
</aside>
<aside class="warning">
Free API key gives you limited access. For single app record calls the limit is 100 hits per day and for
bulk calls you get the first 100 records per call.
</aside>

## Quick Overview

A few quick details about our REST API:

 Type                | Description
-------------------- | --------------
**SSL only**             | We require that all requests are done over SSL.
**UTF-8 encoding**       | We use UTF-8 everywhere.
**Method**               | `GET` for all read calls, `PUT` to submit a new app.
**Version number**       | The current version of our API is v1.
**Multi-records format** | JSON dictionaries separated by newlines also known as JSON Lines (JSONL).
**Date format**          | All dates in the API are strings in the following format: `YYYY-MM-DD`.
**Error handling**       | Errors are returned using [listed HTTP error codes](#errors).
**Bulk API requests**    | Bulk API requests return request ID to validate request:
                         | Request ID is sent via `X-Request-ID` HTTP Header. You may get the status of request using Request Status API.

## Compression

Our REST API allows the use of compression on the request and the response, using the standards
defined by the HTTP 1.1 specification. Some clients will automatically use compression but for
some it has to be turned on manually.

<aside class="success">
Turning on compression can result in speed and size savings of up to 4X.
</aside>

To use compression make sure your requests to our API include the following header
`Accept-Encoding: gzip`. Our API will compress the response if this header is specified. For more
information on how to add this header refer to code examples below.



## Authentication

Requests to the REST API are protected with HTTP Basic authentication. You must provide your API
key to each request made against our API. You can always get a new one <a href='/dashboard/get_api_key/'> here </a>.
If you lost your key you can just enter your email again and we will retrieve it for you.

<aside class="warning">
Requests have to use HTTPS. Using HTTP will return 400 error response.
</aside>

## Errors

The API uses the following error codes:

Error Code | Meaning
---------- | -------
**400** | Bad input parameter or malformed request. The error message should indicate what is specifically wrong.
**401** | Missing or bad API key (email datageeks[at]appmonsta.com if you need a new API key).
**403** | You're requesting something your subscription doesn't cover (email datageeks[at]appmonsta.com if you'd like to change your subscription).
**404** | The data isn't available yet. This may be because we're still collecting it.
**429** | You've exceeded the rate limit for the API you're trying to access. Wait a little or contact datageeks[at]appmonsta.com.
**500** | Something went wrong on our end. Email us at datageeks[at]appmonsta.com with the details of your API request, and we'll troubleshoot it ASAP.

## Platform Specific Fields

Some of the fields are limited to only a particular platform (either Google Play or App Store).
In that case we tag the field description with the appropriate icon:

Icon                                         | Meaning
-------------------------------------------- | --------------------------------------
![android_only](../images/android_logo.jpg)  | Field available only for Android apps.
![itunes_only](../images/itunes_logo.jpg)    | Field available only for iOS apps.

