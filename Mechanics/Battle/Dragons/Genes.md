## Genes
The location of unlocked genes can be found at:
* `0x80145548` in the RAM
* `+e70` in the save file
When using Accession, the selected genes are stored at `0x801463c4` in the RAM. Each gene is one byte. The number of genes used is stored at `0x801463c7` in the RAM. The amount of initial AP the Accession spell uses is stord at `0x801463b8`. Let $T$ be the initial AP cost for using Accession. At the end of every turn, except for the turn in which Ryu uses Accession, $(T+1)/2$ AP is deducted from Ryu's current AP. If Ryu does not have enough AP, then he reverts back to his normal form.

| ID     | Gene     | Affinity                                                   | AP cost |
| ------ | -------- | ---------------------------------------------------------- | ------- |
| `0x00` | Flame    | +1 Flame<br>-1 Frost<br>+1 Dragon                          | 5       |
| `0x01` | Frost    | -1 Flame<br>+1 Frost<br>+1 Dragon                          | 5       |
| `0x02` | Thunder  | +1 Thunder<br>+1 Dragon                                    | 5       |
| `0x03` | Shadow   | +1 Shadow<br>-1 Radiance<br>+1 Dragon                      | 5       |
| `0x04` | Radiance | -1 Shadow<br>+1 Radiance<br>+1 Dragon                      | 5       |
| `0x05` | Force    | -1 HP<br>+1 Power<br>+1 Speed<br>+1 Dragon<br>+1 Warrior   | 8       |
| `0x06` | Defender | +1 HP<br>+1 Defense<br>-1 Speed<br>+1 Dragon<br>+1 Counter | 8       |
| `0x07` | Eldritch | -1 Power<br>+1 Intelligence<br>+1 Dragon                   | 8       |
| `0x08` | Miracle  | +1 HP<br>+1 Power<br>+1 Defense<br>-1 Speed<br>+1 Behemoth | 8       |
| `0x09` | Gross    | +1 HP<br>+1 Power<br>+1 Defense<br>+1 Speed                | 20      |
| `0x0a` | Thorn    |                                                            | 8       |
| `0x0b` | Reverse  |                                                            | 8       |
| `0x0c` | Mutant   |                                                            | 3       |
| `0x0d` | ???      |                                                            | 3       |
| `0x0e` | Trance   |                                                            | 8       |
| `0x0f` | Failure  |                                                            | 1       |
| `0x10` | Fusion   |                                                            | 20      |
| `0x11` | Infinity |                                                            | 40      |
The list of AP cost can be found at:
* `0x800b4c7c` in the RAM
* In the following locations in the game's files:
```
BIN/BATTLE/BATTLE.EMI: 000a847c
BIN/BATTLE/BATTLE2.EMI: 000a847c
BIN/BOSS/BOSS001.EMI: 00065c7c
BIN/BOSS/BOSS002.EMI: 000a947c
BIN/BOSS/BOSS004.EMI: 00065c7c
BIN/BOSS/BOSS007.EMI: 000a847c
BIN/BOSS/BOSS008.EMI: 000a647c
BIN/BOSS/BOSS012.EMI: 000a947c
BIN/BOSS/BOSS013.EMI: 000a947c
BIN/BOSS/BOSS014.EMI: 000a847c
BIN/BOSS/BOSS015.EMI: 000a847c
BIN/BOSS/BOSS017.EMI: 000a947c
BIN/BOSS/BOSS018.EMI: 000a947c
BIN/BOSS/BOSS019.EMI: 000a947c
BIN/BOSS/BOSS020.EMI: 000a947c
BIN/BOSS/BOSS021.EMI: 000a947c
BIN/BOSS/BOSS022.EMI: 00065c7c
BIN/BOSS/BOSS023.EMI: 000a647c
BIN/BOSS/BOSS024.EMI: 000a947c
BIN/BOSS/BOSS025.EMI: 00065c7c
BIN/BOSS/BOSS027.EMI: 000a947c
BIN/BOSS/BOSS028.EMI: 000a947c
BIN/BOSS/BOSS029.EMI: 000a947c
BIN/BOSS/BOSS030.EMI: 000a947c
BIN/BOSS/BOSS031.EMI: 00065c7c
BIN/BOSS/BOSS032.EMI: 000a947c
BIN/BOSS/BOSS033.EMI: 000a847c
BIN/BOSS/BOSS034.EMI: 000a947c
BIN/BOSS/BOSS035.EMI: 000a947c
BIN/BOSS/BOSS036.EMI: 000a947c
BIN/BOSS/BOSS037.EMI: 000a947c
BIN/BOSS/BOSS038.EMI: 000a947c
BIN/BOSS/BOSS040.EMI: 000a947c
BIN/BOSS/BOSS042.EMI: 000a947c
BIN/BOSS/BOSS046.EMI: 000a947c
BIN/BOSS/BOSS047.EMI: 000a947c
BIN/BOSS/BOSS049.EMI: 000a947c
BIN/BOSS/BOSS050.EMI: 000a947c
BIN/BOSS/BOSS051.EMI: 000a947c
BIN/BOSS/BOSS052.EMI: 000a6c7c
BIN/BOSS/BOSS054.EMI: 000a947c
BIN/BOSS/BOSS055.EMI: 000ac47c
```
## Gene Affinity
Genes may have an affinity towards a certain trait. There are 14 traits, some based on an element. When using [[Mechanics/Battle/Dragons/Accession/Accession|Accession]], the affinity table is located at `0x800b6f60` in the RAM.
Each entry is one byte long, one for each affinity.
### Stat Modifiers

| Index  | Affinity     | Stat Effects                                                                          | Abilities                                                                       |
| ------ | ------------ | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `0x00` | Flame        | +1 fire resistance, caps at 7<br>Decreases by 1 at negative levels                    | Flame Breath<br>Flame Claw<br>Inferno (with Intelligence)                       |
| `0x01` | Frost        | +1 ice resistance, caps at 7<br>Ddecreases by 1 at negative levels                    | Frost Breath<br>Frost Claw<br>Blizzard (with Intelligence)                      |
| `0x02` | Thunder      | +1 thunder resistance, caps at 7<br>Decreases by 1 at negative levels                 | Thunder Breath<br>Thunder Claw<br>Myollnir (with Intelligence)                  |
| `0x03` | Shadow       | +2 status resistance<br>+2 death resistance<br>Decreases both by 1 at negative levels | Shadow Breath<br>Chlorine<br>Death (with Intelligence)<br>Ebonfire (with Flame) |
| `0x04` | Radiance     | +1 holy resistance/level, caps at 7<br> Decreases by 1 at negative levels             | Divine Breath<br>Shining Claw<br>Resurrect (with Intelligence)                  |
| `0x05` | HP           | Gives stat bonus to battle HP (see below)                                             |                                                                                 |
| `0x06` | Power        | Gives stat bonus to power (see below)                                                 |                                                                                 |
| `0x07` | Defense      | Gives stat bonus to defense (see below)                                               |                                                                                 |
| `0x08` | Speed        | Gives stat bonus to speed (see below)                                                 |                                                                                 |
| `0x09` | Intelligence | Gives stat bonus to intelligence (see below)                                          | Remedy<br>Restore<br>Vitalize                                                   |
| `0x0a` | Dragon       | At level 1 or below, Ryu becomes a whelp<br>At level 2 or above, Ryu becomes a dragon |                                                                                 |
| `0x0b` | Warrior      | At level 1 or above, Ryu becomes a Warrior                                            | Focus                                                                           |
| `0x0c` | Counter      | None                                                                                  | Counter                                                                         |
| `0x0d` | Behemoth     | At level 1, Ryu becomes a Behemoth                                                    |                                                                                 |
Stat bonuses are additive with respect to the original multiplier. The stat bonuses are given in the table below. The table can be found at:
* `0x800b4e8c` in the RAM
* In the following locations in the game's files:
```
BIN/BATTLE/BATTLE.EMI: 000a868c
BIN/BATTLE/BATTLE2.EMI: 000a868c
BIN/BOSS/BOSS001.EMI: 00065e8c
BIN/BOSS/BOSS002.EMI: 000a968c
BIN/BOSS/BOSS004.EMI: 00065e8c
BIN/BOSS/BOSS007.EMI: 000a868c
BIN/BOSS/BOSS008.EMI: 000a668c
BIN/BOSS/BOSS012.EMI: 000a968c
BIN/BOSS/BOSS013.EMI: 000a968c
BIN/BOSS/BOSS014.EMI: 000a868c
BIN/BOSS/BOSS015.EMI: 000a868c
BIN/BOSS/BOSS017.EMI: 000a968c
BIN/BOSS/BOSS018.EMI: 000a968c
BIN/BOSS/BOSS019.EMI: 000a968c
BIN/BOSS/BOSS020.EMI: 000a968c
BIN/BOSS/BOSS021.EMI: 000a968c
BIN/BOSS/BOSS022.EMI: 00065e8c
BIN/BOSS/BOSS023.EMI: 000a668c
BIN/BOSS/BOSS024.EMI: 000a968c
BIN/BOSS/BOSS025.EMI: 00065e8c
BIN/BOSS/BOSS027.EMI: 000a968c
BIN/BOSS/BOSS028.EMI: 000a968c
BIN/BOSS/BOSS029.EMI: 000a968c
BIN/BOSS/BOSS030.EMI: 000a968c
BIN/BOSS/BOSS031.EMI: 00065e8c
BIN/BOSS/BOSS032.EMI: 000a968c
BIN/BOSS/BOSS033.EMI: 000a868c
BIN/BOSS/BOSS034.EMI: 000a968c
BIN/BOSS/BOSS035.EMI: 000a968c
BIN/BOSS/BOSS036.EMI: 000a968c
BIN/BOSS/BOSS037.EMI: 000a968c
BIN/BOSS/BOSS038.EMI: 000a968c
BIN/BOSS/BOSS040.EMI: 000a968c
BIN/BOSS/BOSS042.EMI: 000a968c
BIN/BOSS/BOSS046.EMI: 000a968c
BIN/BOSS/BOSS047.EMI: 000a968c
BIN/BOSS/BOSS049.EMI: 000a968c
BIN/BOSS/BOSS050.EMI: 000a968c
BIN/BOSS/BOSS051.EMI: 000a968c
BIN/BOSS/BOSS052.EMI: 000a6e8c
BIN/BOSS/BOSS054.EMI: 000a968c
BIN/BOSS/BOSS055.EMI: 000ac68c
```

| Affinity Level | Bonus |
| -------------- | ----- |
| -2             | -50pp |
| -1             | -20pp |
| 0              | 0pp   |
| 1              | 30pp  |
| 2              | 60pp  |
### Ability Sets
The game determines the abilities by checking the affinities. All abilities under all applicable affinity combinations are added to Ryu's ability list. Spells are added from top to bottom. Affinity combinations are checked from top to bottom. The following ability set can be found at:
* `0x800b4eb0` in the RAM
* In the following locations in the game's files:
```
BIN/BATTLE/BATTLE.EMI: 000a86b0
BIN/BATTLE/BATTLE2.EMI: 000a86b0
BIN/BOSS/BOSS001.EMI: 00065eb0
BIN/BOSS/BOSS002.EMI: 000a96b0
BIN/BOSS/BOSS004.EMI: 00065eb0
BIN/BOSS/BOSS007.EMI: 000a86b0
BIN/BOSS/BOSS008.EMI: 000a66b0
BIN/BOSS/BOSS012.EMI: 000a96b0
BIN/BOSS/BOSS013.EMI: 000a96b0
BIN/BOSS/BOSS014.EMI: 000a86b0
BIN/BOSS/BOSS015.EMI: 000a86b0
BIN/BOSS/BOSS017.EMI: 000a96b0
BIN/BOSS/BOSS018.EMI: 000a96b0
BIN/BOSS/BOSS019.EMI: 000a96b0
BIN/BOSS/BOSS020.EMI: 000a96b0
BIN/BOSS/BOSS021.EMI: 000a96b0
BIN/BOSS/BOSS022.EMI: 00065eb0
BIN/BOSS/BOSS023.EMI: 000a66b0
BIN/BOSS/BOSS024.EMI: 000a96b0
BIN/BOSS/BOSS025.EMI: 00065eb0
BIN/BOSS/BOSS027.EMI: 000a96b0
BIN/BOSS/BOSS028.EMI: 000a96b0
BIN/BOSS/BOSS029.EMI: 000a96b0
BIN/BOSS/BOSS030.EMI: 000a96b0
BIN/BOSS/BOSS031.EMI: 00065eb0
BIN/BOSS/BOSS032.EMI: 000a96b0
BIN/BOSS/BOSS033.EMI: 000a86b0
BIN/BOSS/BOSS034.EMI: 000a96b0
BIN/BOSS/BOSS035.EMI: 000a96b0
BIN/BOSS/BOSS036.EMI: 000a96b0
BIN/BOSS/BOSS037.EMI: 000a96b0
BIN/BOSS/BOSS038.EMI: 000a96b0
BIN/BOSS/BOSS040.EMI: 000a96b0
BIN/BOSS/BOSS042.EMI: 000a96b0
BIN/BOSS/BOSS046.EMI: 000a96b0
BIN/BOSS/BOSS047.EMI: 000a96b0
BIN/BOSS/BOSS049.EMI: 000a96b0
BIN/BOSS/BOSS050.EMI: 000a96b0
BIN/BOSS/BOSS051.EMI: 000a96b0
BIN/BOSS/BOSS052.EMI: 000a6eb0
BIN/BOSS/BOSS054.EMI: 000a96b0
BIN/BOSS/BOSS055.EMI: 000ac6b0
```
Each affinity combination has three slots.

| ID     | Affinity Combinations   | Abilities                      |
| ------ | ----------------------- | ------------------------------ |
| `0x00` | Flame                   | Flame Breath<br>Flame Claw     |
| `0x01` | Frost                   | Frost Breath<br>Frost Claw     |
| `0x02` | Thunder                 | Thunder Breath<br>Thunder Claw |
| `0x03` | Shadow                  | Shadow Breath<br>Chlorine      |
| `0x04` | Radiance                | Divine Breath<br>Shining Claw  |
| `0x05` | Flame + Intelligence    | Inferno                        |
| `0x06` | Frost +Intelligence     | Blizzard                       |
| `0x07` | Thunder + Intelligence  | Myollnir                       |
| `0x08` | Shadow + Intelligence   | Death                          |
| `0x09` | Radiance + Intelligence | Resurrect                      |
| `0x0a` | -                       | -                              |
| `0x0b` | Warrior                 | Focus                          |
| `0x0c` | Counter                 | Counter                        |
| `0x0d` | Intelligence            | Remedy<br>Restore<br>Vitalize  |
| `0x0e` | Flame + Shadow          | Ebonfire                       |


