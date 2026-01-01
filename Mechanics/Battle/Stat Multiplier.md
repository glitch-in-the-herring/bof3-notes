Like in Breath of Fire IV, the game keeps track of the current amount of buffs/debuffs applied to the character by using the stat multiplier. 
Except... for some reason this game multiplies the value of the stat multiplier by two before applying them.
## Limit
Normally the limit for buffs is 50 while the limit for debuffs is -25. Multiply by 2 to get the actual amount that you'd expect to see in-game. [[Celerity]] uses a different limit.
```
800a39dc slti   $v0, $v1, 0x0033 ; check if the multiplier is greater than 50
800a39e0 bnez   $v0, 0x800a39f0
800a39e4 addiu  $sp, -0x0008

; if the multiplier is greater than 50
800a39e8 j      0x800a3a00
800a39ec li     $v0, 0x0032 ; cap to 50

800a39f0 slti   $v0, $v1, -0x0019 ; check if the multiplier is less than 25
800a39f4 bnez   $v0, 0x800a3a00 ; if less than -25, cap to -25
800a39f8 li     $v0, -0x0019
800a39fc addu   $v0, $a3, $a2 ;
800a3a00 sb     $v0, 0x0014(a1)
```
The code for the limits can be found at:
* `0x800a39dc` in the RAM
* In the following places in the game's files:
```
BIN/BATTLE/BATTLE.EMI: 000971dc
BIN/BATTLE/BATTLE2.EMI: 000971dc
BIN/BOSS/BOSS001.EMI: 000549dc
BIN/BOSS/BOSS002.EMI: 000981dc
BIN/BOSS/BOSS004.EMI: 000549dc
BIN/BOSS/BOSS007.EMI: 000971dc
BIN/BOSS/BOSS008.EMI: 000951dc
BIN/BOSS/BOSS012.EMI: 000981dc
BIN/BOSS/BOSS013.EMI: 000981dc
BIN/BOSS/BOSS014.EMI: 000971dc
BIN/BOSS/BOSS015.EMI: 000971dc
BIN/BOSS/BOSS017.EMI: 000981dc
BIN/BOSS/BOSS018.EMI: 000981dc
BIN/BOSS/BOSS019.EMI: 000981dc
BIN/BOSS/BOSS020.EMI: 000981dc
BIN/BOSS/BOSS021.EMI: 000981dc
BIN/BOSS/BOSS022.EMI: 000549dc
BIN/BOSS/BOSS023.EMI: 000951dc
BIN/BOSS/BOSS024.EMI: 000981dc
BIN/BOSS/BOSS025.EMI: 000549dc
BIN/BOSS/BOSS027.EMI: 000981dc
BIN/BOSS/BOSS028.EMI: 000981dc
BIN/BOSS/BOSS029.EMI: 000981dc
BIN/BOSS/BOSS030.EMI: 000981dc
BIN/BOSS/BOSS031.EMI: 000549dc
BIN/BOSS/BOSS032.EMI: 000981dc
BIN/BOSS/BOSS033.EMI: 000971dc
BIN/BOSS/BOSS034.EMI: 000981dc
BIN/BOSS/BOSS035.EMI: 000981dc
BIN/BOSS/BOSS036.EMI: 000981dc
BIN/BOSS/BOSS037.EMI: 000981dc
BIN/BOSS/BOSS038.EMI: 000981dc
BIN/BOSS/BOSS040.EMI: 000981dc
BIN/BOSS/BOSS042.EMI: 000981dc
BIN/BOSS/BOSS046.EMI: 000981dc
BIN/BOSS/BOSS047.EMI: 000981dc
BIN/BOSS/BOSS049.EMI: 000981dc
BIN/BOSS/BOSS050.EMI: 000981dc
BIN/BOSS/BOSS051.EMI: 000981dc
BIN/BOSS/BOSS052.EMI: 000959dc
BIN/BOSS/BOSS054.EMI: 000981dc
BIN/BOSS/BOSS055.EMI: 0009b1dc
```