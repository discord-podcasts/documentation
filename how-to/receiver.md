# Listening to a podcast - Being the receiver

For a receiver to connect to a podcast you the podcasts object. This can be given by the [list] endpoint or [podcast]
endpoint.  
Once you have the podcast object you can connect to the websocket with the provided ip and port.

## Socket connection

After connecting you receive the [Hello Event](../resources/events.md#hello-event). It contains the `secretKey` for
decrypting the audio. Now you can start handling audio.  
Before sending the audio you have to clean up your [audio packet](../resources/audio.md). First make sure to remove
the [single prefix byte](../resources/packet.md#packet-types). Then safe your `nonce`, you will need it in a second. Now you
are left with the encrypted audio bytes. Decrypt these bytes using the `secretKey` from
your [Hello Event](../resources/events.md#hello-event) and your saved `nonce`. This data you can then send to Discord.

## Disconnecting

If you want to disconnect just close your connection with any close code.

## Reconnecting

There is no real reconnecting. Once The bytes are received from the sender, they directly get sent back to all receivers.
Just connect like you would for the first time and continue the stream.