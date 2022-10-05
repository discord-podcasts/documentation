# API Reference

The main audio streaming relies on Websockets. This includes:
* sending audio
* receiving audio
* receiving events

Everything else can be done using REST.

* Rest url: `https://podcasts.myra.bot`
* Websocket url: `wss://podcasts.myra.bot`

## Authorization

To be able to use this service you need a **client id** and a **token** which is given to you by us.  
Send these with every request you make as a header.
```
clientId: 1234567890
```
```
token: a_cool_token
```
