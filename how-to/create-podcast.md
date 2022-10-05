# Creating a podcast

In order to create your own podcast, where you can stream to you have to get the connection details of a websocket. This can
be done by requesting a podcast creation.

### Create podcast - POST /podcast

This will response with a [podcast object](../entities/podcast.md) which contains all information about the socket.

## Socket connection

Now that you have all the data you can connect to the websocket. Avoid waiting a long time because podcasts have a timeout.
If no sender connects in a given time your podcast gets closed.  
Connect to the socket and provide the `isSender` header:

```
isSender: true
```

Through the socket you can receive **audio and events**. Make sure to handle both accordingly.

### Packets

All packets you receive contain a prefix byte, which determines whether your packet is a event or audio.
So the packet structure will look like this.

| Description                     | Size    |
|---------------------------------|---------|
| Is audio prefix                 | 1 byte  |
| data   (audio or event details) | m bytes |

| Type  | Byte value |
|-------|------------|
| Event | 0          |
| Audio | 1          |

#### Events

The data bytes can be decoded to a json object. Every event contains a `type` field, which helps you to identify your event.
Here are all possible events.

| Event      | identifier |
|------------|------------|
| Hello      | 0          |
| Disconnect | 1          |

#### Audio

The data bytes are split again into two different things. The nonce for the packet and the encrypted audio data.

| Name  | Size | Description                        |
|-------|------|------------------------------------|
| nonce | 24   | Nonce is used to decrypt the audio |
| audio | n    | Encrypted audio                    |
