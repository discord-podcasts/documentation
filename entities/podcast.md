# Podcast object

## Structure

| Field       | Type    | Description                                         |
|-------------|---------|-----------------------------------------------------|
| id          | String  | Unique ID of the podcast                            |
| port        | Integer | Port of websocket                                   |
| ip          | String  | Ip of websocket                                     |
| activeSince | Long?   | Timestamp since when the podcast is active or null* |
\* Can be null if the sender didn't connect yet

