# Podcast object

### Structure

| Field        | Type  | Description                                         |
|--------------|-------|-----------------------------------------------------|
| id           | u32   | Unique ID of the podcast                            |
| host         | u64   | Client id of the host                               |
| active_since | u128? | Timestamp since when the podcast is active or null* |

\* Can be null if the sender hasn't connected yet

### GET /podcast?id={id}

Returns a [podcast](#structure) matching the id.

### GET /list

Returns an object with all [podcasts](#structure).

| Field    | Type                    | Description  |
|----------|-------------------------|--------------|
| podcasts | [Podcast](#structure)[] | All podcasts |