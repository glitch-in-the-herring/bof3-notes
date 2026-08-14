Furniture means an object on the map that can be interacted with, does not move, and usually looks like a piece of furniture or interior decoration. It can contain items which the player can obtain when interacting with it, such as drawers. [[Chests]] are separate from furniture and often have better rewards. Furniture data is stored in the AREA file.
There are two (known) types of furniture:
* Cabinets, these contain irreplaceable items that the player can take
* Talking furniture, these only show a textbox
Talking furniture can only select a piece of string from:
```
BIN/ETC/AFLDKWA.EMI: 00000800
BIN/ETC/FIRST.EMI: 0003b800
```
## Furniture Data
The data for a furniture contains eight bytes and is structured as such:

| Position | Description                   | Value(s)               | Note                                                                    |
| -------- | ----------------------------- | ---------------------- | ----------------------------------------------------------------------- |
| 0        | x coordinate                  | 8-bit unsigned integer |                                                                         |
| 1        | y coordinate                  | 8-bit unsigned integer |                                                                         |
| 4        | Cabinet ID/Text ID            | 8-bit unsigned integer |                                                                         |
| 5        | Item ID/Furniture Action Type | 8-bit unsigned integer | If this is set to `0x80` then the furniture becomes a talking furniture |
| 6        | Inventory type                | 8-bit unsigned integer |                                                                         |
The base address for the furniture data in each AREA file can be found in:
* `0x8017f974` in the RAM
* `SLUS_004.22: 000e9974` in the game's files
## Switch
The switch for cabinets can be found at:
* `0x80145004` in the RAM
* `+0x92c` in the save file