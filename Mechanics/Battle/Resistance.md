Resistance determines how much damage a combatant takes from attacks. In the case of Holy resistance, it also determines how much healing a combatant receives from a healing spell.
Internally, they are ordered as such:
- Fire
- Ice
- Thunder
- Earth
- Wind
- Holy
- Psionic
- Status
- Death
## Multi-element spells
When a spell has more than one element, the damage taken by the target is the multiplied by the total multiplier of each resistances. For example, if a target's wind resistance is 2 and fire resistance is 2, then the damage taken is $100\%+100\%=200\%$.
## Elemental resistances
Elemental resistance refers to the following resistances:
* Fire
* Ice
* Thunder
* Earth
* Wind
The multipliers for elemental resistances can be found at:
* `0x800b493c` in the RAM
* The following locations in the files:
```
BIN/BATTLE/BATTLE.EMI: 000a813c
BIN/BATTLE/BATTLE2.EMI: 000a813c
BIN/BOSS/BOSS001.EMI: 0006593c
BIN/BOSS/BOSS002.EMI: 000a913c
BIN/BOSS/BOSS004.EMI: 0006593c
BIN/BOSS/BOSS007.EMI: 000a813c
BIN/BOSS/BOSS008.EMI: 000a613c
BIN/BOSS/BOSS012.EMI: 000a913c
BIN/BOSS/BOSS013.EMI: 000a913c
BIN/BOSS/BOSS014.EMI: 000a813c
BIN/BOSS/BOSS015.EMI: 000a813c
BIN/BOSS/BOSS017.EMI: 000a913c
BIN/BOSS/BOSS018.EMI: 000a913c
BIN/BOSS/BOSS019.EMI: 000a913c
BIN/BOSS/BOSS020.EMI: 000a913c
BIN/BOSS/BOSS021.EMI: 000a913c
BIN/BOSS/BOSS022.EMI: 0006593c
BIN/BOSS/BOSS023.EMI: 000a613c
BIN/BOSS/BOSS024.EMI: 000a913c
BIN/BOSS/BOSS025.EMI: 0006593c
BIN/BOSS/BOSS027.EMI: 000a913c
BIN/BOSS/BOSS028.EMI: 000a913c
BIN/BOSS/BOSS029.EMI: 000a913c
BIN/BOSS/BOSS030.EMI: 000a913c
BIN/BOSS/BOSS031.EMI: 0006593c
BIN/BOSS/BOSS032.EMI: 000a913c
BIN/BOSS/BOSS033.EMI: 000a813c
BIN/BOSS/BOSS034.EMI: 000a913c
BIN/BOSS/BOSS035.EMI: 000a913c
BIN/BOSS/BOSS036.EMI: 000a913c
BIN/BOSS/BOSS037.EMI: 000a913c
BIN/BOSS/BOSS038.EMI: 000a913c
BIN/BOSS/BOSS040.EMI: 000a913c
BIN/BOSS/BOSS042.EMI: 000a913c
BIN/BOSS/BOSS046.EMI: 000a913c
BIN/BOSS/BOSS047.EMI: 000a913c
BIN/BOSS/BOSS049.EMI: 000a913c
BIN/BOSS/BOSS050.EMI: 000a913c
BIN/BOSS/BOSS051.EMI: 000a913c
BIN/BOSS/BOSS052.EMI: 000a693c
BIN/BOSS/BOSS054.EMI: 000a913c
BIN/BOSS/BOSS055.EMI: 000ac13c
```
The values are:

| Value | Damage taken |
| ----- | ------------ |
| 0     | 300%         |
| 1     | 200%         |
| 2     | 100%         |
| 3     | 75%          |
| 4     | 50%          |
| 5     | 25%          |
| 6     | 0%           |
| 7     | -100%        |
### Psionic, Status, and Death as an RNG Multiplier
These resistances are used in the [[General Success Rate Formula]]. The values can be found at:
* `0x` in the RAM
* The following locations in the game's files:
```
BIN/BATTLE/BATTLE.EMI: 000a814c
BIN/BATTLE/BATTLE2.EMI: 000a814c
BIN/BOSS/BOSS001.EMI: 0006594c
BIN/BOSS/BOSS002.EMI: 000a914c
BIN/BOSS/BOSS004.EMI: 0006594c
BIN/BOSS/BOSS007.EMI: 000a814c
BIN/BOSS/BOSS008.EMI: 000a614c
BIN/BOSS/BOSS012.EMI: 000a914c
BIN/BOSS/BOSS013.EMI: 000a914c
BIN/BOSS/BOSS014.EMI: 000a814c
BIN/BOSS/BOSS015.EMI: 000a814c
BIN/BOSS/BOSS017.EMI: 000a914c
BIN/BOSS/BOSS018.EMI: 000a914c
BIN/BOSS/BOSS019.EMI: 000a914c
BIN/BOSS/BOSS020.EMI: 000a914c
BIN/BOSS/BOSS021.EMI: 000a914c
BIN/BOSS/BOSS022.EMI: 0006594c
BIN/BOSS/BOSS023.EMI: 000a614c
BIN/BOSS/BOSS024.EMI: 000a914c
BIN/BOSS/BOSS025.EMI: 0006594c
BIN/BOSS/BOSS027.EMI: 000a914c
BIN/BOSS/BOSS028.EMI: 000a914c
BIN/BOSS/BOSS029.EMI: 000a914c
BIN/BOSS/BOSS030.EMI: 000a914c
BIN/BOSS/BOSS031.EMI: 0006594c
BIN/BOSS/BOSS032.EMI: 000a914c
BIN/BOSS/BOSS033.EMI: 000a814c
BIN/BOSS/BOSS034.EMI: 000a914c
BIN/BOSS/BOSS035.EMI: 000a914c
BIN/BOSS/BOSS036.EMI: 000a914c
BIN/BOSS/BOSS037.EMI: 000a914c
BIN/BOSS/BOSS038.EMI: 000a914c
BIN/BOSS/BOSS040.EMI: 000a914c
BIN/BOSS/BOSS042.EMI: 000a914c
BIN/BOSS/BOSS046.EMI: 000a914c
BIN/BOSS/BOSS047.EMI: 000a914c
BIN/BOSS/BOSS049.EMI: 000a914c
BIN/BOSS/BOSS050.EMI: 000a914c
BIN/BOSS/BOSS051.EMI: 000a914c
BIN/BOSS/BOSS052.EMI: 000a694c
BIN/BOSS/BOSS054.EMI: 000a914c
BIN/BOSS/BOSS055.EMI: 000ac14c
```

| Value | Multiplier |
| ----- | ---------- |
| 0     | N/A        |
| 1     | 150        |
| 2     | 100        |
| 3     | 75         |
| 4     | 50         |
| 5     | 25         |
| 6     | 0          |
| 7     | 0          |
