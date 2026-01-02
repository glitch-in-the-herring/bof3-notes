The general table for weapons can be found at at 
- `/BIN/ETC/GAME.EMI: 000340DC` in the files
- `0x801c90dc in the RAM
starting with the Nothing weapon. Each entry is 24 bytes long and can be broken down as such:

| Position | Description       | Value(s)                             | Note                                                                  |
| -------- | ----------------- | ------------------------------------ | --------------------------------------------------------------------- |
| 0-11     | Name              | See the text guide                   |                                                                       |
| 12       | Equipability      | See [[Equipment/Equipability.md]]    |                                                                       |
| 13       | Flags             | See [[Items/General%20Table.md]]     |                                                                       |
| 14       | Icon ID           | 8-bit unsigned integer               |                                                                       |
| 15       | Element           | See [[Mechanics/Battle/Elements.md]] |                                                                       |
| 16       | Weight            | 8-bit unsigned integer               |                                                                       |
| 17       | ?                 |                                      |                                                                       |
| 18       | Power             | 8-bit unsigned integer               |                                                                       |
| 19       | ?                 |                                      |                                                                       |
| 20-21    | Description Index | 16-bit integer                       |                                                                       |
| 22-23    | Buying price      | 16-bit integer                       | Selling price is automatically calculated as half of the buying price |



