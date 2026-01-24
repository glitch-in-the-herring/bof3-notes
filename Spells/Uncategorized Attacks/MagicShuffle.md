| Spell ID         | Targeting | Power | AP  | Element | Battle Spell Call |
| ---------------- | --------- | ----- | --- | ------- | ----------------- |
| `0x25`<br>37<br> | `0xa`*    | 0<br> | 2   | None    | `0x0`             |

\* actual targeting depends on the randomly selected spell

MagicShuffle rolls a $\mathrm{random}(0,31)$ and chooses a random spell from one of the following:

| ID    | Spell      | Probability |
| ----- | ---------- | ----------- |
| 0-7   | Burn       | 25%         |
| 8-9   | Flare      | 12.5%       |
| 10-11 | Frost      | 6.25%       |
| 12    | Cyclone    | 3.125%      |
| 13    | Jolt       | 3.125%      |
| 14    | Simoon     | 3.125%      |
| 15    | Fireblast  | 3.125%      |
| 16    | Iceblast   | 3.125%      |
| 17    | Typhoon    | 3.125%      |
| 18    | Lightning  | 3.125%      |
| 19    | Quake      | 3.125%      |
| 20    | Death      | 3.125%      |
| 21    | Inferno    | 3.125%      |
| 22    | Blizzard   | 3.125%      |
| 23    | Heal       | 3.125%      |
| 24    | Rejuvenate | 3.125%      |
| 25    | Purify     | 3.125%      |
| 26    | Protect    | 3.125%      |
| 27    | Speed      | 3.125%      |
| 28    | Might      | 3.125%      |
| 29    | Sleep      | 3.125%      |
| 30    | Confuse    | 3.125%      |
| 31    | Ebonfire   | 3.125%      |

This table can be found at:
* `0x801eac78` in the RAM
* In the following locations in the game's files:
```
BIN/BATTLE/BATTLE.EMI: 0005d078
BIN/BATTLE/BATTLE2.EMI: 0005d078
BIN/BOSS/BOSS001.EMI: 0001a878
BIN/BOSS/BOSS002.EMI: 0005e078
BIN/BOSS/BOSS004.EMI: 0001a878
BIN/BOSS/BOSS007.EMI: 0005d078
BIN/BOSS/BOSS008.EMI: 0005b078
BIN/BOSS/BOSS012.EMI: 0005e078
BIN/BOSS/BOSS013.EMI: 0005e078
BIN/BOSS/BOSS014.EMI: 0005d078
BIN/BOSS/BOSS015.EMI: 0005d078
BIN/BOSS/BOSS017.EMI: 0005e078
BIN/BOSS/BOSS018.EMI: 0005e078
BIN/BOSS/BOSS019.EMI: 0005e078
BIN/BOSS/BOSS020.EMI: 0005e078
BIN/BOSS/BOSS021.EMI: 0005e078
BIN/BOSS/BOSS022.EMI: 0001a878
BIN/BOSS/BOSS023.EMI: 0005b078
BIN/BOSS/BOSS024.EMI: 0005e078
BIN/BOSS/BOSS025.EMI: 0001a878
BIN/BOSS/BOSS027.EMI: 0005e078
BIN/BOSS/BOSS028.EMI: 0005e078
BIN/BOSS/BOSS029.EMI: 0005e078
BIN/BOSS/BOSS030.EMI: 0005e078
BIN/BOSS/BOSS031.EMI: 0001a878
BIN/BOSS/BOSS032.EMI: 0005e078
BIN/BOSS/BOSS033.EMI: 0005d078
BIN/BOSS/BOSS034.EMI: 0005e078
BIN/BOSS/BOSS035.EMI: 0005e078
BIN/BOSS/BOSS036.EMI: 0005e078
BIN/BOSS/BOSS037.EMI: 0005e078
BIN/BOSS/BOSS038.EMI: 0005e078
BIN/BOSS/BOSS040.EMI: 0005e078
BIN/BOSS/BOSS042.EMI: 0005e078
BIN/BOSS/BOSS046.EMI: 0005e078
BIN/BOSS/BOSS047.EMI: 0005e078
BIN/BOSS/BOSS049.EMI: 0005e078
BIN/BOSS/BOSS050.EMI: 0005e078
BIN/BOSS/BOSS051.EMI: 0005e078
BIN/BOSS/BOSS052.EMI: 0005b878
BIN/BOSS/BOSS054.EMI: 0005e078
BIN/BOSS/BOSS055.EMI: 00061078
```
After it has chosen a spell, it then chooses a target by using the following algorithm:
