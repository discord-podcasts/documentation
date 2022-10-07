# Events

The event bytes can be read as a json object.

### Structure

| Field   | Type        | Description         |
|---------|-------------|---------------------|
| type    | Integer     | Event identifier    |
| content | Json object | Event specific data |


The `type` field tells you what event you received. Here are all possible events.

| Event      | identifier |
|------------|------------|
| Hello      | 0          |
| Disconnect | 1          |

## Hello Event

This event gets received right after connecting. It contains the `secretKey` which is used for encryption/decryption of the
audio packet, together with the `nonce`.

### Structure

| Field     | Type                  | Description                                       |
|-----------|-----------------------|---------------------------------------------------|
| secretKey | Byte array of size 32 | The secret key, used to encrypt/decrypt the audio |