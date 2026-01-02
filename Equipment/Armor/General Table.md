The general table for armor (including helmets and shields) can be found at at 
- `/BIN/ETC/GAME.EMI: 000348A4` in the files
- `0x801c98a4` in the RAM
starting with the Nothing armor. Each entry is 22 bytes long and can be broken down as such:

| Position | Description       | Value(s)                          | Note                                                                  |
| -------- | ----------------- | --------------------------------- | --------------------------------------------------------------------- |
| 0-11     | Name              | See the text guide                |                                                                       |
| 12       | Equipability      | See [[Equipment/Equipability.md]] |                                                                       |
| 13       | Flags             | See [[Items/General%20Table.md]]  |                                                                       |
| 14       | Icon ID           | 8-bit unsigned integer            |                                                                       |
| 15       | Weight            | 8-bit unsigned integer            |                                                                       |
| 16       | Defense           | 8-bit unsigned integer            |                                                                       |
| 17       | ?                 |                                   |                                                                       |
| 18-19    | Description Index | 16-bit integer                    |                                                                       |
| 20-21    | Buying price      | 16-bit integer                    | Selling price is automatically calculated as half of the buying price |
