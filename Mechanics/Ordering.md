There are two party orderings:
* Field ordering
* Battle ordering
In both cases, the IDs used are the same:

| ID     | Character    |
| ------ | ------------ |
| `0x00` | Ryu (young)  |
| `0x01` | Nina (young) |
| `0x02` | Garr         |
| `0x03` | Teepo        |
| `0x04` | Rei          |
| `0x05` | Momo         |
| `0x06` | Peco         |
| `0x07` | Ryu (adult)  |
| `0x08` | Nina (adult) |
| `0xff` | Blank        |
Unlike Breath of Fire IV, the game does not load a new area for battles, which means that the orderings are not reloaded until you enter or exit an area.
## Field Ordering
The field ordering is located at:
* `0x80144f5a-0x80144f5c` in the RAM
* `+0x880` in the save file
Changes to the ordering directly through the RAM does not take effect unless the player enters a new area.
Only necessary field sprites are loaded at any point in the game. Inserting a character into the party that isn't supposed to be loaded at the time (for example: adult Ryu before the timeskip) will cause a crash.
## Battle Ordering 
The battle ordering is located at:
* `0x80144f5d-0x80144f5f` in the RAM
* `+0x883` in the save file
Changes to the battle ordering that involve adding anyone outside of the current field ordering will crash the game.
## Standby
Party members that are not in the current formation are stored at `0x801e6244` in the RAM.