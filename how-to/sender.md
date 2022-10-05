# Creating a podcast - Being the sender

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

## Sending audio

If you received the [Hello event](../resources/events.md#hello-event) you are ready for streaming the audio.

1. Decrypt your received audio form Discord
2. Encrypt the audio with the same nonce as you decrypted it from Discord and the `secretKey` from the Hello event
3. Create a byte array of size `audio` + 1
4. Add the prefix byte to the array, so 1 for audio
5. Add your encrypted audio to the byte array

Finally send your bytes to the websocket. Voilà that's it!