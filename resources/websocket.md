# Websocket

Websocket connections are used to manage a podcast connection. You will need to connect to a websocket first before working
with audio.

### WS /listen

Start listening to a podcast as an audience.

### GET /ws

Host your own podcast.

## Lifecycle

### Hello

Once you connect you will receive a `Hello` event:

| Field      | Type | Description                     |
|------------|------|---------------------------------|
| podcast_id | u32  | The id of the connected podcast |
| port       | u16  | The port of the UDP socket      |

Use this payload to connect to the udp socket. For this use the provided port.

### Connected

Once connected to the UDP socket, you have to send a `Connected` event:

| Field | Type   | Description                 |
|-------|--------|-----------------------------|
| ip    | String | Your remote ip              |
| port  | u16    | The port of your UDP client |

After you've sent this data you're ready to [receive/send audio](audio.md)!

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

ill add the event payloads later sry