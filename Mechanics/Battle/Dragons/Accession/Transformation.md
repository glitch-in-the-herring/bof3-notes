## Predetermined Dragon Forms
When checking for the dragon form to transform into, the game first looks up at the predetermined forms which are stored at:
* `0x800b4d58` in the RAM
* In the following locations in the file:
```
BIN/BATTLE/BATTLE.EMI: 000a8558
BIN/BATTLE/BATTLE2.EMI: 000a8558
BIN/BOSS/BOSS001.EMI: 00065d58
BIN/BOSS/BOSS002.EMI: 000a9558
BIN/BOSS/BOSS004.EMI: 00065d58
BIN/BOSS/BOSS007.EMI: 000a8558
BIN/BOSS/BOSS008.EMI: 000a6558
BIN/BOSS/BOSS012.EMI: 000a9558
BIN/BOSS/BOSS013.EMI: 000a9558
BIN/BOSS/BOSS014.EMI: 000a8558
BIN/BOSS/BOSS015.EMI: 000a8558
BIN/BOSS/BOSS017.EMI: 000a9558
BIN/BOSS/BOSS018.EMI: 000a9558
BIN/BOSS/BOSS019.EMI: 000a9558
BIN/BOSS/BOSS020.EMI: 000a9558
BIN/BOSS/BOSS021.EMI: 000a9558
BIN/BOSS/BOSS022.EMI: 00065d58
BIN/BOSS/BOSS023.EMI: 000a6558
BIN/BOSS/BOSS024.EMI: 000a9558
BIN/BOSS/BOSS025.EMI: 00065d58
BIN/BOSS/BOSS027.EMI: 000a9558
BIN/BOSS/BOSS028.EMI: 000a9558
BIN/BOSS/BOSS029.EMI: 000a9558
BIN/BOSS/BOSS030.EMI: 000a9558
BIN/BOSS/BOSS031.EMI: 00065d58
BIN/BOSS/BOSS032.EMI: 000a9558
BIN/BOSS/BOSS033.EMI: 000a8558
BIN/BOSS/BOSS034.EMI: 000a9558
BIN/BOSS/BOSS035.EMI: 000a9558
BIN/BOSS/BOSS036.EMI: 000a9558
BIN/BOSS/BOSS037.EMI: 000a9558
BIN/BOSS/BOSS038.EMI: 000a9558
BIN/BOSS/BOSS040.EMI: 000a9558
BIN/BOSS/BOSS042.EMI: 000a9558
BIN/BOSS/BOSS046.EMI: 000a9558
BIN/BOSS/BOSS047.EMI: 000a9558
BIN/BOSS/BOSS049.EMI: 000a9558
BIN/BOSS/BOSS050.EMI: 000a9558
BIN/BOSS/BOSS051.EMI: 000a9558
BIN/BOSS/BOSS052.EMI: 000a6d58
BIN/BOSS/BOSS054.EMI: 000a9558
BIN/BOSS/BOSS055.EMI: 000ac558
```
Each form is three bytes long (one for each gene) and there are ... forms. The game checks for the forms 

| Index  | Dragon ID | Genes                                        | Form                                    |
| ------ | --------- | -------------------------------------------- | --------------------------------------- |
| `0x00` | `0x04`    | `11 0e 04`<br>Infinity<br>Trance<br>Radiance | (True) Kaiser                           |
| `0x01` | `0x05`    | `00 01 02`<br>Flame<br>Frost<br>Thunder      | Trygon                                  |
| `0x02` | `0x06`    | `08 0b 0a`<br>Miracle<br>Reverse<br>Thorn    | Wildfire                                |
| `0x03` | `0x06`    | `11 0f ff`<br>Infinity<br>Failure<br>(any)   | (Failed) Kaiser                         |
| `0x04` | `0x08`    | `11 ff ff`<br>Infinity<br>(any)<br>(any)     | (Berserk) Kaiser                        |
| `0x05` | `0x09`    | `0f ff ff`<br>Failure<br>(any)<br>(any)      | (Failed) Whelp                          |
| `0x06` | `0x0a`    | `10 ff ff`<br>Fusion<br>(any)<br>(any)       | See [[Fusion]]<br>This ID is never used |
| `0x06` | `0x0b`    | `03 0e ff`<br>Shadow<br>Trance<br>(any)      | Tiamat<br>                              |
| `0x08` | `0x0c`    | `05 0e ff`<br>Force<br>Trance<br>(any)       | Myrmidon<br>                            |
| `0x09` | `0x0d`    | `08 0d ff`<br>Miracle<br>???<br>(any)        | Mammoth                                 |
| `0x0a` | `0x0e`    | `0c 0d ff`<br>Mutant<br>???<br>(any)         | Pygmy                                   |
The optional (any) gene does not have any effect on the dragon's stats. The game matches the chosen genes to the predetermined forms above by using this algorithm:
1. For $i$ from all of the predetermined dragon forms:
	1. For $j$ from all of $i$'s dragon genes:
		1. For $k$ from all of the selected dragon genes:
			1. Check if $j$ and $k$ match
	2. Go to the next dragon form if none of the genes match
	3. Set the dragon ID $I$ to be the index of the current predetermined dragon form $i + 4$ and end the loop if all of the genes match.

### Fusion
When using the Fusion gene, the game uses this algorithm to check for fusion forms:
1. Load the ID of the first party member that is not Ryu
2. Load the ID of the second party member that is not Ryu
3. Assume that the fusion will primarily be based on the first party member that is not Ryu. Check if the ID of the second party member matches the required ID. If there is a match, then set the dragon ID to the matching fusion form.
4. If the ID does not match with any compatible IDs, then assume that the fusion will primarily be based on the second party member that is not Ryu. Check if the ID of the first party member matches the required ID. If there is a match, then set the dragon ID to the matching fusion form.
5. If the ID does not match with any compatible IDs, then Ryu becomes a normal whelp (ID `0x00`) with no affinities. 
6. If there is a matching extra gene, then Ryu transforms into the "super" variant of that hybrid.

| ID     | Primary | Secondary                    | Extra gene |
| ------ | ------- | ---------------------------- | ---------- |
| `0x0f` | Nina    | Peco<br>Garr                 |            |
| `0x10` | Nina    | Peco<br>Garr                 | Eldritch   |
| `0x11` | Peco    | Garr<br>Rei                  |            |
| `0x12` | Peco    | Garr<br>Rei                  | Shadow     |
| `0x13` | ?       | ?                            | ?          |
| `0x14` | ?       | ?                            | ?          |
| `0x15` | Rei     | Nina<br>Momo<br>Nina (young) |            |
| `0x16` | Rei     | Nina<br>Momo<br>Nina (young) | Force      |
| `0x17` | Momo    | Peco<br>Nina<br>Nina (young) |            |
| `0x18` | Momo    | Peco<br>Nina<br>Nina (young) | ???        |
## Gene Affinity Table
If the selected genes do not fit any of the predetermined dragon forms above, then the gene affinity table is used. See [[Genes#Gene Affinity|Gene Affinity]] for the list of affinities. For each selected gene, the game adds the affinity values to the affinity table. After all of the genes are calculated, the game then checks for these genes:
* Reverse: All of the affinity values are negated
* Thorn: All of the affinity values are doubled
* Mutant: For each non-zero affinity, the game rolls a `random(0,1)`. If it is 0, then the affinity value does not change. If it is 1, the game rolls another `random(0,1)`. If it is 0, then the affinity is decreased by 1. If it is 1, then the affinity value increases by 1.
After all of the affinities are populated, the game then decides on what the dragon ID is using this table. The table is read in order: whichever condition matches first is selected.

| Condition         | Dragon ID | Form     |
| ----------------- | --------- | -------- |
| Behemoth > 0      | `0x03`    | Behemoth |
| Warrior > 0       | `0x02`    | Warrior  |
| Dragon ≥ 2        | `0x01`    | Dragon   |
| None of the above | `0x00`    | Whelp    |
