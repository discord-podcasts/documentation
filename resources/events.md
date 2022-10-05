# Events

Every event contains an integer `type` field, which helps you to identify your event. This field is guaranteed to be in every
event. Here are all possible events.

| Event      | identifier |
|------------|------------|
| Hello      | 0          |
| Disconnect | 1          |

## Hello Event

This event gets received right after connecting.

| Field     | Type   | Description                                       |
|-----------|--------|---------------------------------------------------|
| secretKey | String | The secret key, used to encrypt/decrypt the audio |