As you progress through the game you'll meet masters who grant you new abilities as you level up
## Ordering

| ID     | Name        |
| ------ | ----------- |
| `0x00` | Bunyan      |
| `0x01` | Mygas       |
| `0x02` | Yggdrasil   |
| `0x03` | D'lonzo     |
| `0x04` | Fahl        |
| `0x05` | Durandal    |
| `0x06` | Giotto      |
| `0x07` | Hondara     |
| `0x08` | Emitai      |
| `0x09` | Deis        |
| `0x0a` | Hachio      |
| `0x0b` | Bais        |
| `0x0c` | Lang        |
| `0x0d` | Lee         |
| `0x0e` | Wynn        |
| `0x0f` | Ladon       |
| `0x10` | Meryleep    |
| `0xff` | (no master) |
## Spells
The spells that a master teaches can be found at:
* `0x801d4088` in the RAM
* `BIN/ETC/SISYOU.EMI: 00003c88` in the game's files
Each master has six spell entries. Each spell entry is two bytes in length and consists of:

| Position | Description     |
| -------- | --------------- |
| 1        | Level threshold |
| 2        | Spell ID        |

## Bonuses
The stat bonuses are located at:
* `0x801d4154` in the RAM
* `BIN/ETC/SISYOU.EMI: 00003d54` in the game's files
Each bonus entry consists of:

| Position | Stat |
| -------- | ---- |
| 1        | HP   |
| 2        | AP   |
| 3        | PWR  |
| 4        | DEF  |
| 5        | INT  |
| 6        | AGL  |
## Prerequisites
Some masters require you to meet certain requirements before you unlock them
### Bunyan
### Mygas
Mygas asks for all of your money, regardless of how much you have at hand, as long as it's not zero.
### Yggdrasil
### D'lonzo
D'lonzo requires you to carry 15 different weapons. 
```
80166470 lbu    $v0, 0x0000(a1) ; load weapon ID
80166474 nop    
80166478 beqz   $v0, 0x80166484
8016647c nop    

; If the weapon ID is not zero
80166480 addiu  $a2, 0x0001 ; increment weapon counter

; If the weapon ID is zero
80166484 addiu  $v1, 0x0001 ; increment loop counter
80166488 andi   $v0, $v1, 0x00ff
8016648c sltu   $v0, $a0
80166490 bnez   $v0, 0x80166470
80166494 addiu  $a1, 0x0001
...
801f38e8 sltiu  $v0, 0x000f ; check if weapon counter is greater than or equal to 15
```