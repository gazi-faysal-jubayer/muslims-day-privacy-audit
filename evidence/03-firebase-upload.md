# Google Firebase upload containing email and name

`POST https://app-measurement.com/a` (protobuf, sent by Google Play services). Source: `dump-login4` flow 56.

Printable excerpts around the user-property names (non-printable bytes shown as `.`):

```
.&......4.._id..<kahf-user-id>.+......4..email..<test-email>........4..name..<test-name> .....4(..
.&......4.._id..<kahf-user-id>.+......4..email..<test-email>........4..name..<test-name>........4.
.+......4..email..<test-email>........4..name..<test-name> .....4(.....40.....48.....4B.androidJ.
.+......4..email..<test-email>........4..name..<test-name>........4..platform..android........4..
```

The same values were also found in Google Play services' local upload queue (`google_app_measurement.db`, table `user_attributes`): rows `email`, `name` and `_id` for app `theoaktroop.appoframadan`.
