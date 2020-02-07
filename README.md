# CookieSync documentation

Cookie Synchronization is an important process that allows both SoundCast and a partner to
come to a common understanding about their respective user IDs for the same
user/browser/device. 

It allows us to map SoundCast’s unique cookieIDs to the unique user ID
of our providers.


## If SoundCast initiate the synchronization

SoundCast will call your pixel and you will have to records incoming requests and issues a [302 Redirect](https://en.wikipedia.org/wiki/HTTP_302) to the SoundCast's CookieSync API.

### Url

```
GET https://cookie-sync.api.soundcast.fm/v1/cookie/?partner=[$PARTNER]&uid=[$UID]
```

### Query Parameters

| Parameter | Required | Description    |
| --------- | -------- | -------------- |
| partner   | true     | dsp name       |
| uid       | true     | User cookie ID |

### Example

Soundcast add your pixel on a website.
`<img src="yourdomain.com?pid=42qlwa1&gdpr=1&gdpr_consent={consent_string}">`

You issue a 302 Redirect to the SoundCast CookieSync API
```
GET https://cookie-sync.api.soundcast.fm/v1/cookie/?partner=yourdomain&uid=ql42wa1
```

SoundCast map your user ID with our unique user ID
