# CookieSync documentation

SoundCast can cookie sync with the DSP to enable them to work with our [Supply Side Plateform](https://github.com/SoundCast/soundcast-SSP-documentation).

# Workflows

We allow two different workflows :
* You can use our pixel and we will redirect to query to your servers
* We can call your pixel and you will redirect to our servers

# Request from your pixel

## Url

```
GET https://cookie-sync.api.soundcast.fm/v1/cookie/
```

## Query Parameters

| Parameter | Required | Description    |
|:--------- |:-------- |:-------------- |
| partner   | true     | dsp name       |
| uid       | true     | dsp cookie ID  |

# Example

```
GET https://cookie-sync.api.soundcast.fm/v1/cookie/?partner={$PARTNER}&uid={$UID}
```

# Request from our pixel

On this workflow, you will have to use the standart macro **$UID**

## Url

```
GET https://cookie-sync.api.soundcast.fm/v1/cookie/sync
```

## Query Parameters

| Parameter | Required | Description                |
|:--------- |:-------- |:-------------------------- |
| url       | true     | url to redirect the query  |

# Example

```
GET https://cookie-sync.api.soundcast.fm/v1/cookie/?partner={DSP_NAME}&uid={DSP_COOKIE_ID}
```
