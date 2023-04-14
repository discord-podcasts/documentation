# Audio packets

Audio packets are from Discord and therefore encoded with [Opus](https://www.opus-codec.org/) and encrypted with
xsalsa20_poly1305. It's important that you move your nonce to the first 24 bytes, so that every client can decrypt the bytes
correctly.

### Structure

| Name  | Size     | Description                               |
|-------|----------|-------------------------------------------|
| nonce | 24 bytes | Nonce, which is used to decrypt the audio |
| audio | n bytes  | Encrypted audio                           |