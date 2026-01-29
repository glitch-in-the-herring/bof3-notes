| Spell ID     | Targeting | Power | AP  | Element | Battle Spell Call |
| ------------ | --------- | ----- | --- | ------- | ----------------- |
| `0x24`<br>36 | `0xa`*    | 0<br> | 2   | None    | `0x0`             |

\* actual targeting depends on the randomly selected spell
Recall rolls a $\mathrm{random}(0,31)$ and chooses a random spell from one of the following:

| ID    | Spell     | Probability |
| ----- | --------- | ----------- |
| 0-15  | Burn      | 50%         |
| 16-17 | Flare     | 6.25%       |
| 18-19 | Frost     | 6.25%       |
| 20    | Cyclone   | 3.125%      |
| 21    | Jolt      | 3.125%      |
| 22    | Simoon    | 3.125%      |
| 23    | Fireblast | 3.125%      |
| 24    | Iceblast  | 3.125%      |
| 25    | Typhoon   | 3.125%      |
| 26    | Lightning | 3.125%      |
| 27    | Heal      | 3.125%      |
| 28    | Purify    | 3.125%      |
| 29    | Protect   | 3.125%      |
| 30    | Speed     | 3.125%      |
| 31    | Might     | 3.125%      |


This table can be found at:
* `0x801eac58` in the RAM
* In the following locations in the game's files:
```
BIN/BATTLE/BATTLE.EMI: 0005d058
BIN/BATTLE/BATTLE2.EMI: 0005d058
BIN/BOSS/BOSS001.EMI: 0001a858
BIN/BOSS/BOSS002.EMI: 0005e058
BIN/BOSS/BOSS004.EMI: 0001a858
BIN/BOSS/BOSS007.EMI: 0005d058
BIN/BOSS/BOSS008.EMI: 0005b058
BIN/BOSS/BOSS012.EMI: 0005e058
BIN/BOSS/BOSS013.EMI: 0005e058
BIN/BOSS/BOSS014.EMI: 0005d058
BIN/BOSS/BOSS015.EMI: 0005d058
BIN/BOSS/BOSS017.EMI: 0005e058
BIN/BOSS/BOSS018.EMI: 0005e058
BIN/BOSS/BOSS019.EMI: 0005e058
BIN/BOSS/BOSS020.EMI: 0005e058
BIN/BOSS/BOSS021.EMI: 0005e058
BIN/BOSS/BOSS022.EMI: 0001a858
BIN/BOSS/BOSS023.EMI: 0005b058
BIN/BOSS/BOSS024.EMI: 0005e058
BIN/BOSS/BOSS025.EMI: 0001a858
BIN/BOSS/BOSS027.EMI: 0005e058
BIN/BOSS/BOSS028.EMI: 0005e058
BIN/BOSS/BOSS029.EMI: 0005e058
BIN/BOSS/BOSS030.EMI: 0005e058
BIN/BOSS/BOSS031.EMI: 0001a858
BIN/BOSS/BOSS032.EMI: 0005e058
BIN/BOSS/BOSS033.EMI: 0005d058
BIN/BOSS/BOSS034.EMI: 0005e058
BIN/BOSS/BOSS035.EMI: 0005e058
BIN/BOSS/BOSS036.EMI: 0005e058
BIN/BOSS/BOSS037.EMI: 0005e058
BIN/BOSS/BOSS038.EMI: 0005e058
BIN/BOSS/BOSS040.EMI: 0005e058
BIN/BOSS/BOSS042.EMI: 0005e058
BIN/BOSS/BOSS046.EMI: 0005e058
BIN/BOSS/BOSS047.EMI: 0005e058
BIN/BOSS/BOSS049.EMI: 0005e058
BIN/BOSS/BOSS050.EMI: 0005e058
BIN/BOSS/BOSS051.EMI: 0005e058
BIN/BOSS/BOSS052.EMI: 0005b858
BIN/BOSS/BOSS054.EMI: 0005e058
BIN/BOSS/BOSS055.EMI: 00061058
```