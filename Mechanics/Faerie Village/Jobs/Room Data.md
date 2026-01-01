Not to be confused with [[Faerie Job Data]], which is tied to individual faeries, the room data is tied to individual rooms. They can be found at:
* `0x801457a0` in the RAM
The first entry is reserved for the idle faeries. Each entry is 8 bytes long and is structured as such:

| Position | Description                        | Values                                                                                                                                                                                | Notes |
| -------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| 0        | Job type                           | `0x04`: Scholar<br>`0x05`: Merchant<br>`0x06`: Inn<br>`0x07`: Gift shop<br>`0x08`: Fortune<br>`0x09`: Explorer<br>`0x0a`: Antiques<br>`0x0b`: Music<br>`0x0c`: Casino<br>`0x0d`: Copy |       |
| 1        | Job subtype                        |                                                                                                                                                                                       |       |
| 2        | Job subsubtype                     |                                                                                                                                                                                       |       |
| 3        | Unknown                            |                                                                                                                                                                                       |       |
| 4-7      | Number of battles since last visit | 16-bit unsigned integer                                                                                                                                                               |       |
