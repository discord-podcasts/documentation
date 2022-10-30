# Podcast object

### Structure

| Field       | Type    | Description                                         |
|-------------|---------|-----------------------------------------------------|
| id          | Integer | Unique ID of the podcast                            |
| host        | String  | Client id of the host                               |
| activeSince | Long?   | Timestamp since when the podcast is active or null* |

\* Can be null if the sender hasn't connected yet

### GET /podcast?id={id}

Returns a [podcast](#structure) matching the id.

### GET /list

Returns a json array with all active [podcasts](#structure).

### POST /podcast

Creates a new podcast to connect to. Returns the newly created [podcast](#structure).