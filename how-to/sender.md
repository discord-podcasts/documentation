# Creating a podcast - Being the sender

Being the sender requires you to be able to receive voice data by discord. Sadly this is undocumented. Some libraries do
support it though. Use them or write your own implementation based on their projects:

* [Kord](https://github.com/kordlib/kord)
* [Pycord](https://github.com/Pycord-Development/pycord)

In order to stream your audio you have to request a podcast. This can be done by
[requesting a podcast creation](../resources/podcast.md#post-podcast). This will response with a
[podcast object](../resources/podcast.md) which contains the id.

## Socket connection

Now that you have all the data you can connect to the websocket. Avoid waiting a long time because podcasts have a timeout.
If no sender connects in a given time your podcast gets closed.  
Connect to the socket and provide
* The podcast id as a query parameter
* A `clientId` header with your client id
* A `token` header with your token
* A`isHost` header

```
wss://podcasts.myra.bot?id={id}

clientId: 012345
token: ab12?!
isHost: true
```

Through the websocket you only receive events.

## Sending audio

If you received the [Hello event](../resources/events.md#hello-event) you are ready for streaming the audio.

1. Decrypt your received audio form Discord
2. Encrypt the audio with the same nonce as you decrypted it from Discord and the `secretKey` from the Hello event
3. Create a byte array of size `audio` + 1
4. Add the prefix byte to the array, so 1 for audio
5. Add your encrypted audio to the byte array

Finally, send your bytes to the websocket. Voilà that's it!