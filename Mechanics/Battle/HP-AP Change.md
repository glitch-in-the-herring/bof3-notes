During battle, the game stores the change in HP/AP in a location in the battle data.
For the player's party, these are located at:
* HP: `+0x11c` from the battle data start
* AP: `+0x11e` from the battle data start
For the enemy's party, these are located at:
* HP:
* AP: 
## Change Text
The text that shows when HP/AP is changed depends on the heal status. 

| Byte   | Description |
| ------ | ----------- |
| `0x01` | Heal HP     |
| `0x02` | Heal AP     |
### HP change text
HP change text reads 
### AP change text