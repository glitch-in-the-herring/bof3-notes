The general table for spells can be found at at 
- `/BIN/ETC/GAME.EMI: 0003570B` in the files
- `0x801ca71c` in the RAM
starting with the empty spell (not to be confused with the [[Noting]] spells). Each entry in the table is 20 bytes long and can be broken down as such:

| Position | Description                       | Value(s)                                        | Note                                                                               |
| -------- | --------------------------------- | ----------------------------------------------- | ---------------------------------------------------------------------------------- |
| 0-11     | Name                              | See the text guide                              |                                                                                    |
| 12       | Targeting                         | See [[Targeting]]                               |                                                                                    |
| 13       | Difficulty and spell category[^1] | High bit: Difficulty<br>Low bit: Spell category |                                                                                    |
| 14       | AP cost                           | 8-bit unsigned integer                          |                                                                                    |
| 15       | Power                             | 8-bit unsigned integer                          | Unlike in Breath of Fire IV, the power is actually used for some buffs and debuffs |
| 16       | Element                           | See [[Elements]]                                |                                                                                    |
| 17       |                                   |                                                 |                                                                                    |
| 18-19    | Description Index                 | 16-bit integer                                  |                                                                                    |

[^1]: Found by Thegreatben
	
