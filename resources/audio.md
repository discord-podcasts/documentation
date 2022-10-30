# Audio packets

Audio packets are from Discord and therefore encoded with [Opus](https://www.opus-codec.org/) and encrypted with
xsalsa20_poly1305. In our case it doesn't matter how we generate the nonce because when sending/receiving the audio the nonce
will always be moved to the second to 25th byte.

### Structure

| Name  | Size     | Description                          |
|-------|----------|--------------------------------------|
| nonce | 24 bytes | Nonce is used to decrypt the audio   |
| audio | n bytes  | Encrypted audio                      |