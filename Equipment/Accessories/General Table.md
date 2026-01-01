The general table for accessories can be found at at 
- `/BIN/ETC/GAME.EMI: 00034E7C` in the files
- `0x801c9e7c` in the RAM
starting with the Nothing accessory. Each entry is 20 bytes long and can be broken down as such:

| Position | Description       | Value(s)                | Note                                                                  |
| -------- | ----------------- | ----------------------- | --------------------------------------------------------------------- |
| 0-11     | Name              | See the text guide      |                                                                       |
| 12       | ?                 |                         |                                                                       |
| 13       | ?                 |                         |                                                                       |
| 14       | ?                 |                         |                                                                       |
| 15       | Weight            | 8-bit unsigned integer  |                                                                       |
| 16-17    | Description index | 16-bit unsigned integer |                                                                       |
| 18-19    | Buying price      | 16-bit unsigned integer | Selling price is automatically calculated as half of the buying price |


