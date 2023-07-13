# Websocket

Websocket connections are used to manage a podcast connection. You will need to connect to a websocket first before working
with audio.

### WS /listen

Start listening to a podcast as an audience.

### GET /ws

Host your own podcast.

## Lifecycle

Connect to the websocket and await the [Hello Event](#hello). This event provides the information to connect to the audio
socket. Connect to the audio socket and send a [Connected event](#connected). Once you've sent this you will receive
a [Client Join Event](#client-connect), which shows that you managed to connect successfully to both the websocket and the
udp
server.  
Now you're ready to [receive/send audio](audio.md)!

## Events

After sending the Connected Event you can receive events.  
Each event has a matching event type code which are listed here.

| Code | Event        |
|------|--------------|
| 1    | Hello        |
| 2    | Connected    |
| 3    | Disconnected |
| 4    | ClientJoin   |
| 5    | End          |

Events are structured like so:

| Field | Type   | Description                                                      |
|-------|--------|------------------------------------------------------------------|
| t     | u16    | The event code                                                   |
| data  | Object | Event data, this depends on the event itself and is listed below |

### Hello

Once you connect you will receive a `Hello` event:

| Field      | Type   | Description                     |
|------------|--------|---------------------------------|
| podcast_id | u32    | The id of the connected podcast |
| ip         | String | Ip address of UDP socket        |
| port       | u16    | The port of the UDP socket      |

Use this payload to connect to the udp socket. For this use the provided port.

### Connected

Once connected to the UDP socket, you have to send a `Connected` event:

| Field | Type   | Description                 |
|-------|--------|-----------------------------|
| ip    | String | Your remote ip              |
| port  | u16    | The port of your UDP client |

> **Note**: Discord needs your ip as well, so the Discord API wrappers will do some sort of Ip discovery too. If you have
> trouble finding out your Ip, just use the one your Discord API wrapper provides.

### Client Disconnect

This event gets send after a client disconnected from the websocket.

| Field     | Type | Description                            |
|-----------|------|----------------------------------------|
| client_id | u32  | The client id of the client which left |

### Client Connect

This event gets send when a new client starts connected to the podcasts audio socket.

| Field     | Type | Description                              |
|-----------|------|------------------------------------------|
| client_id | u32  | The Client id of the newly joined client |

### End

This event gets send when the host leaves the podcast. With this the podcasts ends.  
The payload is an empty object.