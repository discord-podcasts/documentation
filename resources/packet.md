# Packets

All packets you receive contain a prefix byte, which determines whether your packet is an event or audio.
So the packet structure will look like this.

### Structure

| Description                     | Size    |
|---------------------------------|---------|
| Is audio prefix                 | 1 byte  |
| data   (audio or event details) | n bytes |

### Packet types

| Type               | Byte value |
|--------------------|------------|
| [Event](events.md) | 0          |
| [Audio](audio.md)  | 1          |