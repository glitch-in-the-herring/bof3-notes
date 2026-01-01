| Spell ID         | Targeting                           | Power    | AP  | Element        | Battle Spell Call |
| ---------------- | ----------------------------------- | -------- | --- | -------------- | ----------------- |
| `0x43`<br>67<br> | `0x3a`<br>All<br>Always enemy party | -12*<br> | 4   | Ice<br>Psionic | `0x24`            |
\* Treated as a signed integer
Chill does two things:
* It deals Ice damage using the [[Magic Formula]], with the power set by the battle spell call. By default this is 20.
* It reduces the targets' speed based on the spell's power, times two for some reason, and uses the [[General Success Rate Formula]] to calculate the success of the debuff. This happens a few frames after the damage.

```
8009eed0 li     $a2, 0x0014 ; loads 20 as the spell power
``` 
This code can be found at:
```
BIN/BATTLE/BATTLE.EMI: 000926d0
BIN/BATTLE/BATTLE2.EMI: 000926d0
BIN/BOSS/BOSS001.EMI: 0004fed0
BIN/BOSS/BOSS002.EMI: 000936d0
BIN/BOSS/BOSS004.EMI: 0004fed0
BIN/BOSS/BOSS007.EMI: 000926d0
BIN/BOSS/BOSS008.EMI: 000906d0
BIN/BOSS/BOSS012.EMI: 000936d0
BIN/BOSS/BOSS013.EMI: 000936d0
BIN/BOSS/BOSS014.EMI: 000926d0
BIN/BOSS/BOSS015.EMI: 000926d0
BIN/BOSS/BOSS017.EMI: 000936d0
BIN/BOSS/BOSS018.EMI: 000936d0
BIN/BOSS/BOSS019.EMI: 000936d0
BIN/BOSS/BOSS020.EMI: 000936d0
BIN/BOSS/BOSS021.EMI: 000936d0
BIN/BOSS/BOSS022.EMI: 0004fed0
BIN/BOSS/BOSS023.EMI: 000906d0
BIN/BOSS/BOSS024.EMI: 000936d0
BIN/BOSS/BOSS025.EMI: 0004fed0
BIN/BOSS/BOSS027.EMI: 000936d0
BIN/BOSS/BOSS028.EMI: 000936d0
BIN/BOSS/BOSS029.EMI: 000936d0
BIN/BOSS/BOSS030.EMI: 000936d0
BIN/BOSS/BOSS031.EMI: 0004fed0
BIN/BOSS/BOSS032.EMI: 000936d0
BIN/BOSS/BOSS033.EMI: 000926d0
BIN/BOSS/BOSS034.EMI: 000936d0
BIN/BOSS/BOSS035.EMI: 000936d0
BIN/BOSS/BOSS036.EMI: 000936d0
BIN/BOSS/BOSS037.EMI: 000936d0
BIN/BOSS/BOSS038.EMI: 000936d0
BIN/BOSS/BOSS040.EMI: 000936d0
BIN/BOSS/BOSS042.EMI: 000936d0
BIN/BOSS/BOSS046.EMI: 000936d0
BIN/BOSS/BOSS047.EMI: 000936d0
BIN/BOSS/BOSS049.EMI: 000936d0
BIN/BOSS/BOSS050.EMI: 000936d0
BIN/BOSS/BOSS051.EMI: 000936d0
BIN/BOSS/BOSS052.EMI: 00090ed0
BIN/BOSS/BOSS054.EMI: 000936d0
BIN/BOSS/BOSS055.EMI: 000966d0
```