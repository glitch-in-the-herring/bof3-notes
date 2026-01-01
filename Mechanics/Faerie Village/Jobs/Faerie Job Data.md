Each job data is attached to a single faerie, not the room that the faerie is in. The data can be found at:
* `0x801455c8` in the RAM
Each entry is 8 bytes long and is structured as such:

| Position | Description                                                   | Values                                                                                                                | Notes |
| -------- | ------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ----- |
| 0        | Status                                                        | `0x00`: Dead<br>`0x01`: Alive                                                                                         |       |
| 1        | Room                                                          | `0x00`: Idle<br>`0x01-0x08`: Job rooms (left-right then top-bottom)<br>`0x09`: Hunt<br>`0x0a`: Clear<br>`0x0b`: Build |       |
| 2-3      | Job-specific data                                             |                                                                                                                       |       |
| 4-7      | Number of battles fought when last interacting with this shop |                                                                                                                       |       |
