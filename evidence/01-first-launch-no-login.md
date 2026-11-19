# First launch, not logged in

## Facebook: MOBILE_APP_INSTALL sent at first launch

`POST https://graph.facebook.com/v16.0/746655931311044/activities` → HTTP 200  
Source: `dump` flow 53

User-Agent: `FBAndroidSDK.18.1.3`

Request:
```json
access_token=746655931311044|<client-token>
format=json
sdk=android
event=MOBILE_APP_INSTALL
anon_id=<anon-id>
application_tracking_enabled=true
advertiser_id_collection_enabled=true
extinfo=["a2","theoaktroop.appoframadan",292,"6.4.1","14","sdk_gphone64_x86_64","en_","GMT+06:00","T-Mobile",1080,2209,"2.62",4,6,5,"Asia\/Dhaka"]
application_package_name=theoaktroop.appoframadan

```

## Facebook: fb_mobile_activate_app

`POST https://graph.facebook.com/v16.0/746655931311044/activities` → HTTP 200  
Source: `dump` flow 54

User-Agent: `FBAndroidSDK.18.1.3`

Request:
```json
format=json
sdk=android
custom_events=[{"_eventName":"fb_mobile_activate_app","_logTime":1795073721,"_ui":"SplashActivity","_session_id":"<uuid>","fb_mobile_launch_source":"Unclassified"}]
operational_parameters=[{"iap_parameters":{"is_implicit_purchase_logging_enabled":"1","is_autolog_app_events_enabled":"1"}}]
event=CUSTOM_APP_EVENTS
anon_id=<anon-id>
application_tracking_enabled=true
advertiser_id_collection_enabled=true
extinfo=["a2","theoaktroop.appoframadan",292,"6.4.1","14","sdk_gphone64_x86_64","en_","GMT+06:00","T-Mobile",1080,2209,"2.62",4,6,5,"Asia\/Dhaka"]
application_package_name=theoaktroop.appoframadan

```

## Kahf backend: device registration (city/country before location permission)

`POST https://backend.muslimsday.com/api/v1/devices` → HTTP 201  
Source: `dump` flow 72

User-Agent: `ktor-client`

Request:
```json
{
  "device_id": "<uuid>",
  "platform": "android",
  "fcm_token": "<fcm-token>",
  "flags": {
    "app_language": "bn",
    "content_language": "bn",
    "country": "Bangladesh",
    "city": "Dhaka",
    "theme": "system_default",
    "platform": "android",
    "app_version": "6.4.1",
    "push_enabled": false
  }
}
```

## Kahf OpenPanel: first event (note the fake "Pixel 8" User-Agent)

`POST https://op.kahf.co.uk/api/track` → HTTP 200  
Source: `dump` flow 63

User-Agent: `Mozilla/5.0 (Linux; Android 14; Pixel 8) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/120.0.6099.230 Mobile Safari/537.36 MuslimsDay/1.0`

Request:
```json
{
  "type": "track",
  "payload": {
    "name": "screen_view",
    "deviceId": "<uuid>",
    "timestamp": "2026-11-19T07:35:24.144Z",
    "properties": {
      "platform": "android",
      "app_version": "6.4.1",
      "build_number": "292",
      "flavor": "prod",
      "language": "bn",
      "theme_mode": "light",
      "subscription_tier": "none",
      "__path": "location_selection",
      "__title": "location_selection",
      "path": "location_selection",
      "title": "location_selection",
      "screen_name": "location_selection",
      "screen_class": "LocationSelectionScreen",
      "session_id": "<uuid>"
    }
  }
}
```

## Firebase Remote Config: clarity_enabled = true

`POST https://firebaseremoteconfig.googleapis.com/v1/projects/872821252495/namespaces/firebase:fetch` → HTTP 200  
Source: `dump` flow 68

User-Agent: `Dalvik/2.1.0 (Linux; U; Android 14; sdk_gphone64_x86_64 Build/UE1A.230829.050)`

Response:
```json
{
  "entries": {
    "clarity_enabled": "true",
    "flash_offer_enabled": "true",
    "openpanel_api_url": "https://your-selfhosted-domain/api",
    "openpanel_client_id": "<your project's client ID>",
    "openpanel_enabled": "true",
    "openpanel_min_app_version": "6.1.0",
    "openpanel_verbose_logging": "false",
    "remove_ads_fab_enabled": "true"
  },
  "appName": "theoaktroop.appoframadan",
  "state": "UPDATE",
  "experimentDescriptions": [
    {
      "experimentId": "_exp_abt_4",
      "variantId": "0",
      "triggerEvent": "onboarding_location_continue",
      "experimentStartTime": "2026-11-15T03:21:22.116411Z",
      "triggerTimeoutMillis": "15552000000",
      "timeToLiveMillis": "15552000000",
      "affectedParameterKeys": [
        "flash_offer_enabled"
      ]
    },
    {
      "experimentId": "_exp_rollout_1",
      "variantId": "1",
      "experimentStartTime": "2026-05-20T12:17:27.448820Z",
      "triggerTimeoutMillis": "15552000000",
      "timeToLiveMillis": "15552000000"
    },
    {
      "experimentId": "_exp_rollout_2",
      "variantId": "1",
      "experimentStartTime": "2026-09-01T01:32:18.366776Z",
      "triggerTimeoutMillis": "15552000000",
      "timeToLiveMillis": "15552000000"
    }
  ],
  "templateVersion": "15",
  "rolloutMetadata": [
    {
      "rolloutId": "rollout_1",
      "variantId": "1",
      "affectedParameterKeys": [
        "openpanel_enabled"
      ]
    },
    {
      "rolloutId": "rollout_2",
      "variantId": "1",
      "affectedParameterKeys": [
        "clarity_enabled"
      ]
    }
  ]
}
```

## Microsoft Clarity config: maskingMode 0 (= Balanced)

`GET https://www.clarity.ms/tag/mobile/xsccj95q8n` → HTTP 200  
Source: `dump` flow 527

User-Agent: `Dalvik/2.1.0 (Linux; U; Android 14; sdk_gphone64_x86_64 Build/UE1A.230829.050)`

Response:
```json
{
  "ingestUrl": "https://i.clarity.ms/",
  "reportUrl": "",
  "activate": true,
  "lean": false,
  "lightMode": false,
  "maskingMode": 0,
  "webMask": [],
  "webUnmask": [],
  "nativeMask": [],
  "nativeUnmask": [],
  "webViewCapture": {
    "allowedUrls": [],
    "disallowedUrls": [],
    "disableCapture": false
  },
  "screenCapture": {
    "allowedScreens": [],
    "disallowedScreens": []
  },
  "network": {
    "allowMeteredNetwork": false,
    "maxDataVolume": null
  },
  "lowEndDevices": {
    "disableRecordings": false
  },
  "imageCompression": {
    "format": 2,
    "quality": 70
  },
  "analyticsStorage": true,
  "adsStorage": true
}
```
