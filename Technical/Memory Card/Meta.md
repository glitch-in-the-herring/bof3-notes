The memory card's metadata is whatever data that isn't used directly in the gameplay.
## Save File Name
The save file name is found at `+0xea0` from the start of the save file. The name is limited to five characters. It is overwritten by whatever name Ryu has whenever the game is saved.
## Portraits
The portraits of the active party members are found at `+0xea5`. Each portrait is one byte. There are three portraits. The IDs are:

| ID     | Portrait      |
| ------ | ------------- |
| `0x00` | Ryu (young)   |
| `0x01` | Nina (young)  |
| `0x02` | Garr          |
| `0x03` | Teepo         |
| `0x04` | Rei           |
| `0x05` | Momo          |
| `0x06` | Peco          |
| `0x07` | Ryu (adult)   |
| `0x08` | Nina (adult)  |
| `0x09` | Ryu (pajamas) |
| `0x0a` | Whelp         |
| `0x0b` | Rei (adult)   |
| `0xff` | Blank         |
## Level
The save's level is found at `+0xea8` from the start of the save file. This is automatically set to Ryu's current level when saving the game.

## Timer
The timer is found at `+0xeac` from the start of the save file. It uses the [[Clock]] format. It is automatically set to the actual timer when saving the game.
