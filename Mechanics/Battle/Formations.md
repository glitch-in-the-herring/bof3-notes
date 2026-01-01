Formations determine the position of combatants during battle and gives buffs/debuffs. The current formation is stored at:
* `0x80144f58` in the RAM
* `+0x880` in the memory card
There are six formations:

| ID  | Name    |
| --- | ------- |
| 0   | Normal  |
| 1   | Attack  |
| 2   | Defense |
| 3   | Chain   |
| 4   | Magic   |
| 5   | Refuge  |
The bit switch for unlocked formations is found at:
* `0x80144f59` in the RAM
* `+0x881` in the memory card
For the probabilities of each position being targeted by the enemy (under normal conditions), see [[Target]].
## Normal
The base formation. 
## Attack

| 1st            | 2nd | 3rd |
| -------------- | --- | --- |
| PWR +50%       | -   | -   |
| DEF -25%       | -   | -   |
| Reprisal +100% | -   | -   |

Increases the first party member's PWR by 50% while decreasing their DEF by 25%
## Defense
| 1st | 2nd | 3rd |
| --- | --- | --- |
| -   | -   | -   |
Surprisingly, this formation does *not* change the defense stat of the party members. Instead, what it does is it takes the calculated physical damage of an attack and subtracts 25% of it. The code that checks this is:
```
801dc604 li     $v0, 0x0002 ; defense formation = 2
801dc608 lui    $v1, 0x8014
801dc60c lbu    $v1, 0x4f58(v1) ; load the current formation
801dc610 nop    
801dc614 bne    $v1, $v0, 0x801dc62c ; if the current formation is defense
801dc618 andi   $v0, $s2, 0x0080

801dc61c sll    $v0, $s1, 0x10
801dc620 sra    $v0, 0x12 ; calculate dmg / 4
801dc624 subu   $s1, $v0 ; calculate dmg - dmg / 4
```
And can be found at:
```
BIN/BATTLE/BATTLE.EMI: 0004ea0c
BIN/BATTLE/BATTLE2.EMI: 0004ea0c
BIN/BOSS/BOSS001.EMI: 0000c20c
BIN/BOSS/BOSS002.EMI: 0004fa0c
BIN/BOSS/BOSS004.EMI: 0000c20c
BIN/BOSS/BOSS007.EMI: 0004ea0c
BIN/BOSS/BOSS008.EMI: 0004ca0c
BIN/BOSS/BOSS012.EMI: 0004fa0c
BIN/BOSS/BOSS013.EMI: 0004fa0c
BIN/BOSS/BOSS014.EMI: 0004ea0c
BIN/BOSS/BOSS015.EMI: 0004ea0c
BIN/BOSS/BOSS017.EMI: 0004fa0c
BIN/BOSS/BOSS018.EMI: 0004fa0c
BIN/BOSS/BOSS019.EMI: 0004fa0c
BIN/BOSS/BOSS020.EMI: 0004fa0c
BIN/BOSS/BOSS021.EMI: 0004fa0c
BIN/BOSS/BOSS022.EMI: 0000c20c
BIN/BOSS/BOSS023.EMI: 0004ca0c
BIN/BOSS/BOSS024.EMI: 0004fa0c
BIN/BOSS/BOSS025.EMI: 0000c20c
BIN/BOSS/BOSS027.EMI: 0004fa0c
BIN/BOSS/BOSS028.EMI: 0004fa0c
BIN/BOSS/BOSS029.EMI: 0004fa0c
BIN/BOSS/BOSS030.EMI: 0004fa0c
BIN/BOSS/BOSS031.EMI: 0000c20c
BIN/BOSS/BOSS032.EMI: 0004fa0c
BIN/BOSS/BOSS033.EMI: 0004ea0c
BIN/BOSS/BOSS034.EMI: 0004fa0c
BIN/BOSS/BOSS035.EMI: 0004fa0c
BIN/BOSS/BOSS036.EMI: 0004fa0c
BIN/BOSS/BOSS037.EMI: 0004fa0c
BIN/BOSS/BOSS038.EMI: 0004fa0c
BIN/BOSS/BOSS040.EMI: 0004fa0c
BIN/BOSS/BOSS042.EMI: 0004fa0c
BIN/BOSS/BOSS046.EMI: 0004fa0c
BIN/BOSS/BOSS047.EMI: 0004fa0c
BIN/BOSS/BOSS049.EMI: 0004fa0c
BIN/BOSS/BOSS050.EMI: 0004fa0c
BIN/BOSS/BOSS051.EMI: 0004fa0c
BIN/BOSS/BOSS052.EMI: 0004d20c
BIN/BOSS/BOSS054.EMI: 0004fa0c
BIN/BOSS/BOSS055.EMI: 00052a0c
```
## Chain

| 1st           | 2nd       | 3rd       |
| ------------- | --------- | --------- |
| SPD unchanged | SPD = 1st | SPD = 1st |
| DEF -50%      | DEF -50%  | DEF -50%  |
Chain sets the speed of everyone in the party equal to the first member while cutting everyone's defense in half.
## Magic
| 1st      | 2nd      | 3rd      |
| -------- | -------- | -------- |
| INT -25% | INT -25% | INT +50% |
Magic increases the third party member's intelligence while lowering the others.
## Refuge
Heals 1 HP every turn.