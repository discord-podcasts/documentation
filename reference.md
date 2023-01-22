# API Reference

The API is split into 3 different parts: Websockets, UDP and REST:
1. Each podcast connection requires its own websocket session which is responsible for receiving and sending events.
2. Audio receiving and sending is done over a udp socket.
3. Everything else can be done using REST.

* Rest url: `https://podcasts.myra.bot`
* Websocket url: `wss://podcasts.myra.bot`

## Authorization

To be able to use this service you need a **client id** and a **client secret** which is given to you by us.  
Send these with every request you make as a header.
```
client_id: 1234567890
```
```
client_secret: a_cool_secret
```
