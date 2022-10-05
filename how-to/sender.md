# Creating a podcast

Being the sender requires you to be able to receive voice data by discord. Sadly this is undocumented. Some libraries do
support it though. Use them or write your own implementation based on their projects:

* [Kord](https://github.com/kordlib/kord)
* [Pycord](https://github.com/Pycord-Development/pycord)

In order to create your own podcast, where you can stream to you have to get the connection details of a websocket. This can
be done by requesting a podcast creation.

### Create podcast - POST /podcast

This will response with a [podcast object](../resources/podcast.md) which contains all information about the socket.

## Socket connection

Now that you have all the data you can connect to the websocket. Avoid waiting a long time because podcasts have a timeout.
If no sender connects in a given time your podcast gets closed.  
Connect to the socket and provide the `isSender` header:

```
isSender: true
```

Through the socket you can receive **audio and events**. Make sure to handle both accordingly.

## Packets

All packets you receive contain a prefix byte, which determines whether your packet is a event or audio.
So the packet structure will look like this.

| Description                     | Size    |
|---------------------------------|---------|
| Is audio prefix                 | 1 byte  |
| data   (audio or event details) | n bytes |

| Type  | Byte value |
|-------|------------|
| Event | 0          |
| Audio | 1          |

### Events

The data bytes can be decoded to a json object. Every event contains a `type` field, which helps you to identify your event.
Here are all possible events.

| Event      | identifier |
|------------|------------|
| Hello      | 0          |
| Disconnect | 1          |

Get a full list of events [here](../resources/events.md).

### Audio

The data bytes are split again into two different things. The nonce for the packet and the encrypted audio data.

| Name  | Size     | Description                        |
|-------|----------|------------------------------------|
| nonce | 24 bytes | Nonce is used to decrypt the audio |
| audio | n bytes  | Encrypted audio                    |

If you received the [Hello event](../resources/events.md#-hello-event) you are ready for streaming the audio.

1. Decrypt your received audio form Discord
2. Encrypt the audio with the same nonce as you decrypted it from Discord and the `secretKey` from the Hello event
3. Create a byte array of size `audio` + 1
4. Add the prefix byte to the array, so 1 for audio
5. Add your encrypted audio to the byte array

Finally send your bytes to the websocket. Voilà that's it!