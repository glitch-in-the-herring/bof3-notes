Spell calls are functions that are called by spells to calculate their effects.
## Battle spell calls
The battle spell call table can be found at:
* `0x800b44f8` in the RAM
* In the following locations in the game's files:
```
BIN/BATTLE/BATTLE.EMI: 000a7cf8
BIN/BATTLE/BATTLE2.EMI: 000a7cf8
BIN/BOSS/BOSS001.EMI: 000654f8
BIN/BOSS/BOSS002.EMI: 000a8cf8
BIN/BOSS/BOSS004.EMI: 000654f8
BIN/BOSS/BOSS007.EMI: 000a7cf8
BIN/BOSS/BOSS008.EMI: 000a5cf8
BIN/BOSS/BOSS012.EMI: 000a8cf8
BIN/BOSS/BOSS013.EMI: 000a8cf8
BIN/BOSS/BOSS014.EMI: 000a7cf8
BIN/BOSS/BOSS015.EMI: 000a7cf8
BIN/BOSS/BOSS017.EMI: 000a8cf8
BIN/BOSS/BOSS018.EMI: 000a8cf8
BIN/BOSS/BOSS019.EMI: 000a8cf8
BIN/BOSS/BOSS020.EMI: 000a8cf8
BIN/BOSS/BOSS021.EMI: 000a8cf8
BIN/BOSS/BOSS022.EMI: 000654f8
BIN/BOSS/BOSS023.EMI: 000a5cf8
BIN/BOSS/BOSS024.EMI: 000a8cf8
BIN/BOSS/BOSS025.EMI: 000654f8
BIN/BOSS/BOSS027.EMI: 000a8cf8
BIN/BOSS/BOSS028.EMI: 000a8cf8
BIN/BOSS/BOSS029.EMI: 000a8cf8
BIN/BOSS/BOSS030.EMI: 000a8cf8
BIN/BOSS/BOSS031.EMI: 000654f8
BIN/BOSS/BOSS032.EMI: 000a8cf8
BIN/BOSS/BOSS033.EMI: 000a7cf8
BIN/BOSS/BOSS034.EMI: 000a8cf8
BIN/BOSS/BOSS035.EMI: 000a8cf8
BIN/BOSS/BOSS036.EMI: 000a8cf8
BIN/BOSS/BOSS037.EMI: 000a8cf8
BIN/BOSS/BOSS038.EMI: 000a8cf8
BIN/BOSS/BOSS040.EMI: 000a8cf8
BIN/BOSS/BOSS042.EMI: 000a8cf8
BIN/BOSS/BOSS046.EMI: 000a8cf8
BIN/BOSS/BOSS047.EMI: 000a8cf8
BIN/BOSS/BOSS049.EMI: 000a8cf8
BIN/BOSS/BOSS050.EMI: 000a8cf8
BIN/BOSS/BOSS051.EMI: 000a8cf8
BIN/BOSS/BOSS052.EMI: 000a64f8
BIN/BOSS/BOSS054.EMI: 000a8cf8
BIN/BOSS/BOSS055.EMI: 000abcf8
```

| ID     | Location | Effect                                                                  | Target |
| ------ | -------- | ----------------------------------------------------------------------- | ------ |
| `0x00` |          |                                                                         |        |
| `0x04` |          | Calculates the [[Magic Formula]]                                        | HP     |
| `0x06` |          | Calculates the [[Breath Formula]] with spell rank 3 and defense penalty | HP     |
| `0x40` |          | Calculates the [[Breath Formula]] with spell rank 3                     | HP     |
| `0x41` |          | Calculates the [[Breath Formula]] with spell rank 1                     | HP     |
| `0x42` |          | Calculates the [[Breath Formula]] with spell rank 2                     | HP     |
| `0x49` |          | Calculates the Melee Formula with                                       | HP     |
| `0x70` |          | Drain to 1                                                              | HP     |
| `0x72` |          | Calculates the [[Magic Formula]]                                        | AP     |
| `0x7c` |          | Calculates the [[Breath Formula]] with spell rank 2 and defense penalty | HP     |
 