# CookieSync documentation

Cookie Synchronization is an important process that allows both SoundCast and a partner to
come to a common understanding about their respective user IDs for the same
user/browser/device. 

It allows us to map SoundCast’s unique cookieIDs to the unique user ID
of our providers.

We support two workflows
* [SoundCast initiate the synchronization](#soundCast-initiate-the-synchronization)
* [You initiate the synchronization](#you-initiate-the-synchronization)


## SoundCast initiate the synchronization

SoundCast will call your pixel and you will have to record incoming requests and issues a [302 Redirect](https://en.wikipedia.org/wiki/HTTP_302) to the SoundCast's CookieSync API.

### Url

```
GET https://cookie-sync.api.soundcast.fm/v1/cookie/?partner=${PARTNER}&uid=${UID}
```

### Query Parameters

| Parameter | Required | Description    |
| --------- | -------- | -------------- |
| partner   | true     | dsp name       |
| uid       | true     | User cookie ID |

### Example

Soundcast add your pixel on a website.
```
<img src="yourdomain.com?pid=42qlwa1&gdpr=1&gdpr_consent=${CONSENT}">
```

You issue a 302 Redirect to the SoundCast CookieSync API
```
GET https://cookie-sync.api.soundcast.fm/v1/cookie/?partner=yourdomain&uid=ql42wa1
```

SoundCast map your user ID with our unique user ID

## You initiate the synchronization

You will call our pixel and SoundCast will record incoming requests and issues a [302 Redirect](https://en.wikipedia.org/wiki/HTTP_302) to your user matching API. Your API will need a **UID** placeholder in it's URL to receive the SoundCast unique user ID.

### TAG

```
<img src="https://cookie-sync.api.soundcast.fm/v1/fwd/?url=$URL">
```

### Query Parameters

| Parameter | Required | Description                |
|:--------- |:-------- |:-------------------------- |
| url       | true     | Your callback URL. Soundcast will redirect the queries to this URL after applying our unique user ID in the **UID** placeholder in the url with a [302 Redirect](https://en.wikipedia.org/wiki/HTTP_302) HTTP status code |

### Example

By placing this pixel on a website
```
<img src='https://cookie-sync.api.soundcast.fm/v1/fwd/?url=callback.yourdomain.com?uid=$UID' />
```

SoundCast will replace the **$uid** by its unique user ID and issue a 302 Redirect to the url of the query.
```
GET https://callback.yourdomain.com?uid=ql42wa1
```
