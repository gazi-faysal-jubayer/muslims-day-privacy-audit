# Server-side retention and the "delete qaza data" button

App data was wiped (`pm clear`), then the same account signed in again. Everything below came back from the server.

## Habits: prayer ticks restored with exact timestamps

`GET https://backend.muslimsday.com/api/v1/habits/sync?since=0&limit=500` → HTTP 200  
Source: `dump-probe` flow 834

User-Agent: `ktor-client`

Response:
```json
{
  "server_changes": {
    "entries": [
      {
        "date": "2026-11-19",
        "code": 1,
        "key": "fajr",
        "completed": true,
        "client_updated_at": "2026-11-19T08:12:16.961Z",
        "updated_seq": 1122299
      },
      {
        "date": "2026-11-19",
        "code": 2,
        "key": "dhuhr",
        "completed": true,
        "client_updated_at": "2026-11-19T08:12:21.214Z",
        "updated_seq": 1122305
      }
    ],
    "days": [
      {
        "date": "2026-11-19",
        "is_fasting_day": false,
        "is_tarawih_day": false,
        "timezone": "Asia/Dhaka",
        "client_updated_at": "2026-11-19T08:12:21.214Z",
        "updated_seq": 1122304
      }
    ],
    "amal_progress": [
      {
        "item_id": 402,
        "date": "2026-11-19",
        "count_total": 5,
        "read_total": 0,
        "listened_total": 0,
        "manual_total": 0,
        "goal": 100,
        "completed": false,
        "updated_seq": 1122336
      }
    ]
  },
  "cursor": 1122336,
  "has_more": false
}
```

## Dhikr progress restored

`GET https://backend.muslimsday.com/api/v1/habits/challenges/progress?from=2026-10-20&to=2026-11-19` → HTTP 200  
Source: `dump-probe` flow 836

User-Agent: `ktor-client`

Response:
```json
{
  "progress": [
    {
      "item_id": 402,
      "date": "2026-11-19",
      "count_total": 5,
      "read_total": 0,
      "listened_total": 0,
      "manual_total": 0,
      "goal": 100,
      "completed": false,
      "updated_seq": 1122336
    }
  ],
  "goals": []
}
```

## Qaza balances restored

`GET https://backend.muslimsday.com/api/v1/qaza/state?today=2026-11-19` → HTTP 200  
Source: `dump-probe` flow 842

User-Agent: `ktor-client`

Response:
```json
{
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
  "summary": {
    "salat_remaining": 25032,
    "salat_made_up_total": 0,
    "fast_remaining": 0,
    "this_week_made_up": 0,
    "streak_days": 0,
    "avg_made_up_per_day_30d": null,
    "first_event_date": "2026-11-19"
  },
  "settings": {
    "count_witr": true,
    "track_salat": false,
    "track_fasts": false,
    "pace": {
      "mode": "with_each_prayer"
    },
    "fast_goal": {
      "mode": "before_ramadan"
    },
    "setup": null,
    "habit_checkin_enabled": true,
    "hide_numbers": {
      "home": false,
      "notifications": false
    },
    "fast_buckets": []
  },
  "features": {
    "estimator": true,
    "reminders": true,
    "insights": true,
    "home_card": true,
    "widgets": true,
    "extra_fast_kinds": true,
    "export": true
  },
  "cursor": 14183
}
```

## Qaza sync: settings list empty (birth date/gender not stored)

`GET https://backend.muslimsday.com/api/v1/qaza/sync?since=0&limit=500` → HTTP 200  
Source: `dump-probe` flow 843

User-Agent: `ktor-client`

Response:
```json
{
  "server_changes": {
    "balances": [
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
    "settings": [],
    "habit_resolutions": []
  },
  "cursor": 14183,
  "has_more": false
}
```

## "Delete qaza data" sends negative corrections; history kept (opening_total stays 4172)

`POST https://backend.muslimsday.com/api/v1/qaza/sync` → HTTP 200  
Source: `dump-probe` flow 965

User-Agent: `ktor-client`

Request:
```json
{
  "since": 14183,
  "today": "2026-11-19",
  "events": [
    {
      "event_id": "<uuid>",
      "kind": "fajr",
      "type": "correction",
      "count": -4172,
      "local_date": "2026-11-19",
      "source": "manual",
      "client_created_at": 1795078529934
    },
    {
      "event_id": "<uuid>",
      "kind": "dhuhr",
      "type": "correction",
      "count": -4172,
      "local_date": "2026-11-19",
      "source": "manual",
      "client_created_at": 1795078529966
    },
    {
      "event_id": "<uuid>",
      "kind": "asr",
      "type": "correction",
      "count": -4172,
      "local_date": "2026-11-19",
      "source": "manual",
      "client_created_at": 1795078530035
    },
    {
      "event_id": "<uuid>",
      "kind": "maghrib",
      "type": "correction",
      "count": -4172,
      "local_date": "2026-11-19",
      "source": "manual",
      "client_created_at": 1795078530179
    },
    {
      "event_id": "<uuid>",
      "kind": "isha",
      "type": "correction",
      "count": -4172,
      "local_date": "2026-11-19",
      "source": "manual",
      "client_created_at": 1795078530244
    },
    {
      "event_id": "<uuid>",
      "kind": "witr",
      "type": "correction",
      "count": -4172,
      "local_date": "2026-11-19",
      "source": "manual",
      "client_created_at": 1795078530261
    }
  ],
  "settings": [],
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
  "settings_rejected": [],
  "resolutions_superseded": [],
  "resolutions_rejected": [],
  "balances": [
    {
      "kind": "fajr",
      "bucket_id": "",
      "remaining": 0,
      "opening_total": 4172,
      "missed_total": 0,
      "made_up_total": 0,
      "correction_total": -4172,
      "updated_seq": 14220
    },
    {
      "kind": "dhuhr",
      "bucket_id": "",
      "remaining": 0,
      "opening_total": 4172,
      "missed_total": 0,
      "made_up_total": 0,
      "correction_total": -4172,
      "updated_seq": 14219
    },
    {
      "kind": "asr",
      "bucket_id": "",
      "remaining": 0,
      "opening_total": 4172,
      "missed_total": 0,
      "made_up_total": 0,
      "correction_total": -4172,
      "updated_seq": 14218
    },
    {
      "kind": "maghrib",
      "bucket_id": "",
      "remaining": 0,
      "opening_total": 4172,
      "missed_total": 0,
      "made_up_total": 0,
      "correction_total": -4172,
      "updated_seq": 14222
    },
    {
      "kind": "isha",
      "bucket_id": "",
      "remaining": 0,
      "opening_total": 4172,
      "missed_total": 0,
      "made_up_total": 0,
      "correction_total": -4172,
      "updated_seq": 14221
    },
    {
      "kind": "witr",
      "bucket_id": "",
      "remaining": 0,
      "opening_total": 4172,
      "missed_total": 0,
      "made_up_total": 0,
      "correction_total": -4172,
      "updated_seq": 14223
    }
  ],
  "daily_totals": [],
  "summary": {
    "salat_remaining": 0,
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
  "cursor": 14223,
  "has_more": false
}
```

## Kahf ID: every reinstall registers a new device (limit 2)

`POST https://id.kahf.co/graphql` → HTTP 200  
Source: `dump-probe` flow 1408

User-Agent: `ktor-client`

Response:
```json
{
  "errors": [
    {
      "message": "Remove a device at https://id.kahf.co/devices to add this one",
      "locations": [
        {
          "line": 3,
          "column": 13
        }
      ],
      "path": [
        "createDevice"
      ],
      "extensions": {
        "code": "DEVICE_LIMIT",
        "kind": "own_device",
        "limit": 2,
        "used": 2
      }
    }
  ],
  "data": {
    "createDevice": null
  }
}
```
