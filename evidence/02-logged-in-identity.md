# Logged in with a throwaway Kahf ID

## Kahf OpenPanel: identify call, email used as profileId

`POST https://op.kahf.co.uk/api/track` → HTTP 200  
Source: `dump-login3` flow 23

User-Agent: `Mozilla/5.0 (Linux; Android 14; Pixel 8) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/120.0.6099.230 Mobile Safari/537.36 MuslimsDay/1.0`

Request:
```json
{
  "type": "identify",
  "payload": {
    "profileId": "<test-email>",
    "deviceId": "<uuid>",
    "email": "<test-email>",
    "firstName": "<test-name>"
  }
}
```

## Kahf OpenPanel: every later event is filed under the email

```
track    screen_view                        profileId=-  {}
track    login_success                      profileId=<test-email>  {"user_id": "<kahf-user-id>", "email": "<test-email>", "method": "social"}
track    premium_upsell_shown               profileId=-  {"subscription_tier": "none", "source": "more_gift", "is_logged_in": true}
identify                                    profileId=<test-email>  {}
track    kahf_id_login_success              profileId=<test-email>  {"subscription_tier": "none"}
track    menu_item_click                    profileId=<test-email>  {"subscription_tier": "none", "item": "HOME"}
track    screen_view                        profileId=<test-email>  {"subscription_tier": "none", "screen_name": "HOME", "screen_class": "MainScreen"}
track    screen_view                        profileId=<test-email>  {"subscription_tier": "none", "screen_name": "new_home_screen", "screen_class": "HomeScreen"}
track    prayer_track_checkbox_clicked      profileId=<test-email>  {"subscription_tier": "none", "waqt": 0, "checked": true, "is_logged_in": true}
track    prayer_track_checkbox_clicked      profileId=<test-email>  {"subscription_tier": "none", "waqt": 2, "checked": true, "is_logged_in": true}
track    screen_view                        profileId=<test-email>  {"subscription_tier": "none", "screen_name": "daily_amal_session", "screen_class": "DailyAmalSessionScreen"}
track    daily_amal_open                    profileId=<test-email>  {"subscription_tier": "none", "amal_type": "counter", "habit_code": 19, "entry_point": "home_card"}
track    screen_view                        profileId=<test-email>  {"subscription_tier": "none", "screen_name": "HOME", "screen_class": "MainScreen"}
track    screen_view                        profileId=<test-email>  {"subscription_tier": "none", "screen_name": "new_home_screen", "screen_class": "HomeScreen"}
track    menu_item_click                    profileId=<test-email>  {"subscription_tier": "none", "item": "UTILITY"}
track    screen_view                        profileId=<test-email>  {"subscription_tier": "none", "screen_name": "UTILITY", "screen_class": "MainScreen"}
track    helpful_apps_section_view          profileId=<test-email>  {"subscription_tier": "none", "app_count": 3}
track    action_taken_from_tools            profileId=<test-email>  {"subscription_tier": "none"}
track    qaza_open                          profileId=<test-email>  {"subscription_tier": "none", "entry_point": "utility"}
track    screen_view                        profileId=<test-email>  {"subscription_tier": "none", "screen_name": "qaza", "screen_class": "QazaTrackerScreen"}
track    qaza_hint_shown                    profileId=<test-email>  {"subscription_tier": "none", "hint_id": "witr"}
track    qaza_estimator_step                profileId=<test-email>  {"subscription_tier": "none", "step": 1, "action": "next"}
track    qaza_estimator_step                profileId=<test-email>  {"subscription_tier": "none", "step": 2, "action": "next"}
track    qaza_estimator_step                profileId=<test-email>  {"subscription_tier": "none", "step": 3, "action": "next"}
track    screen_view                        profileId=-  {"subscription_tier": "none", "screen_name": "new_home_screen", "screen_class": "HomeScreen"}
track    screen_view                        profileId=-  {"subscription_tier": "none", "screen_name": "HOME", "screen_class": "MainScreen"}
identify                                    profileId=<test-email>  {}
```

## Microsoft Clarity: identity tags and device signals inside the session upload (`j.clarity.ms/collect`, gzip)

```
"<!>BuildBoard",["goldfish_x86_64"]
"<!>BuildDevice",["emu64xa"]
"<!>BuildHardware",["ranchu"]
"<!>BuildModel",["sdk_gphone64_x86_64"]
"<!>DisplayMetricsDensityDpi",["420"]
"<!>SettingsGlobalADBEnabled",["true"]
"<!>SettingsGlobalBootCount",["2"]
"<!>SettingsGlobalDevelopmentSettingsEnabled",["false"]
[0,34,"email",["<test-email>"]]
[0,34,"name",["<test-name>"]]
[0,34,"userId",["<kahf-user-id>"]]
```

## Formbricks (form.kahf.co): user attributes

`POST https://form.kahf.co/api/v2/client/cmudpq6vl01f2017zaw4bktwr/user` → HTTP 403  
Source: `dump-login3` flow 16

User-Agent: `okhttp/5.3.2`

Request:
```json
{
  "userId": "<kahf-user-id>",
  "attributes": {
    "is_premium": "true",
    "is_ansar": "false",
    "platform": "Android",
    "app_version": "292",
    "country": "Bangladesh",
    "is_logged_in": "true"
  }
}
```

Response:
```json
{
  "code": "forbidden",
  "message": "User identification is only available for enterprise users.",
  "details": {}
}
```

## Kahf backend: session

`POST https://backend.muslimsday.com/api/v1/auth/sessions` → HTTP 201  
Source: `dump-login3` flow 13

User-Agent: `ktor-client`

Request:
```json
{
  "device_id": "<uuid>",
  "platform": "android",
  "app_version": "6.4.1",
  "kahf_expires_in": 2591993,
  "kahf_user_id": "<kahf-user-id>"
}
```

## Kahf backend: device now linked to the Kahf user

`POST https://backend.muslimsday.com/api/v1/devices` → HTTP 200  
Source: `dump-login3` flow 21

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
    "city": "Dhaka, Dhaka District",
    "theme": "system_default",
    "platform": "android",
    "app_version": "6.4.1",
    "push_enabled": true
  },
  "kahf_user_id": "<kahf-user-id>"
}
```

## Kahf backend: prayer ticks synced

`POST https://backend.muslimsday.com/api/v1/habits/sync` → HTTP 200  
Source: `dump-login3` flow 54

User-Agent: `ktor-client`

Request:
```json
{
  "since": 0,
  "limit": 500,
  "days": [
    {
      "date": "2026-11-19",
      "is_fasting_day": false,
      "is_tarawih_day": false,
      "timezone": "Asia/Dhaka",
      "client_updated_at": 1795075936961
    }
  ],
  "changes": [
    {
      "date": "2026-11-19",
      "code": 1,
      "completed": true,
      "client_updated_at": 1795075936961
    }
  ],
  "amal_events": []
}
```

## Kahf backend: dhikr (Istighfar) count synced

`POST https://backend.muslimsday.com/api/v1/habits/sync` → HTTP 200  
Source: `dump-login3` flow 67

User-Agent: `ktor-client`

Request:
```json
{
  "since": 1122305,
  "limit": 500,
  "days": [],
  "changes": [],
  "amal_events": [
    {
      "event_id": "<uuid>",
      "item_id": 402,
      "date": "2026-11-19",
      "metric": "count",
      "source": "session",
      "delta": 5,
      "goal": 100,
      "client_created_at": 1795075962934
    }
  ]
}
```

## Kahf backend: qaza estimate + birth date/gender (server rejects "profile")

`POST https://backend.muslimsday.com/api/v1/qaza/sync` → HTTP 200  
Source: `dump-login3` flow 121

User-Agent: `ktor-client`

Request:
```json
{
  "since": 0,
  "today": "2026-11-19",
  "events": [
    {
      "event_id": "<uuid>",
      "kind": "fajr",
      "type": "opening",
      "count": 4172,
      "local_date": "2026-11-19",
      "source": "estimator",
      "client_created_at": 1795076118124
    },
    {
      "event_id": "<uuid>",
      "kind": "dhuhr",
      "type": "opening",
      "count": 4172,
      "local_date": "2026-11-19",
      "source": "estimator",
      "client_created_at": 1795076118124
    },
    {
      "event_id": "<uuid>",
      "kind": "asr",
      "type": "opening",
      "count": 4172,
      "local_date": "2026-11-19",
      "source": "estimator",
      "client_created_at": 1795076118124
    },
    {
      "event_id": "<uuid>",
      "kind": "maghrib",
      "type": "opening",
      "count": 4172,
      "local_date": "2026-11-19",
      "source": "estimator",
      "client_created_at": 1795076118124
    },
    {
      "event_id": "<uuid>",
      "kind": "isha",
      "type": "opening",
      "count": 4172,
      "local_date": "2026-11-19",
      "source": "estimator",
      "client_created_at": 1795076118124
    },
    {
      "event_id": "<uuid>",
      "kind": "witr",
      "type": "opening",
      "count": 4172,
      "local_date": "2026-11-19",
      "source": "estimator",
      "client_created_at": 1795076118124
    }
  ],
  "settings": [
    {
      "key": "profile",
      "value": {
        "birth_date": "1995-03-07",
        "gender": "male"
      },
      "client_updated_at": 1795076116193
    }
  ],
  "device_id": "<uuid>"
}
```

Response:
```json
{
  "accepted": [
    "<uuid>",
    "<uuid>",
    "<uuid>",
    "<uuid>",
    "<uuid>",
    "<uuid>"
  ],
  "rejected": [],
  "settings_superseded": [],
  "settings_rejected": [
    {
      "key": "profile",
      "code_reason": "unknown_setting"
    }
  ],
  "resolutions_superseded": [],
  "resolutions_rejected": [],
  "balances": [
    {
      "kind": "fajr",
      "bucket_id": "",
      "remaining": 4172,
      "opening_total": 4172,
      "missed_total": 0,
      "made_up_total": 0,
      "correction_total": 0,
      "updated_seq": 14180
    },
    {
      "kind": "dhuhr",
      "bucket_id": "",
      "remaining": 4172,
      "opening_total": 4172,
      "missed_total": 0,
      "made_up_total": 0,
      "correction_total": 0,
      "updated_seq": 14179
    },
    {
      "kind": "asr",
      "bucket_id": "",
      "remaining": 4172,
      "opening_total": 4172,
      "missed_total": 0,
      "made_up_total": 0,
      "correction_total": 0,
      "updated_seq": 14178
    },
    {
      "kind": "maghrib",
      "bucket_id": "",
      "remaining": 4172,
      "opening_total": 4172,
      "missed_total": 0,
      "made_up_total": 0,
      "correction_total": 0,
      "updated_seq": 14182
    },
    {
      "kind": "isha",
      "bucket_id": "",
      "remaining": 4172,
      "opening_total": 4172,
      "missed_total": 0,
      "made_up_total": 0,
      "correction_total": 0,
      "updated_seq": 14181
    },
    {
      "kind": "witr",
      "bucket_id": "",
      "remaining": 4172,
      "opening_total": 4172,
      "missed_total": 0,
      "made_up_total": 0,
      "correction_total": 0,
      "updated_seq": 14183
    }
  ],
  "daily_totals": [],
  "summary": {
    "salat_remaining": 25032,
    "salat_made_up_total": 0,
    "fast_remaining": 0,
    "this_week_made_up": 0,
    "streak_days": 0,
    "avg_made_up_per_day_30d": null,
    "first_event_date": "2026-11-19"
  },
  "server_changes": {
    "balances": [],
    "daily_totals": [],
    "settings": [],
    "habit_resolutions": []
  },
  "cursor": 14183,
  "has_more": false
}
```
