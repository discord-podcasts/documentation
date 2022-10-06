# Webscoket

## Disconencts

You as a receiver and sender can get disconnected. All known reasons are listen below.

| Title                    | Code | Description                                   |
|--------------------------|------|-----------------------------------------------|
| Missing auth             | 4000 | Authentication headers are missing            |
| Invalid auth             | 4001 | Invalid authentication data                   |
| Invalid payload          | 4002 | The sender send an invalid payload            |
| Sender disconnected      | 4003 | The sender disconnected                       |
| Sender already connected | 4004 | A sender is already connected to this podcast |
| Sender timeout           | 4005 | No sender connected during the time limit     |
| Unknown podcast          | 4006 | No podcast found                              |
