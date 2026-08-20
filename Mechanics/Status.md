A party member or a combatant can be afflicted with a status effect.

| Bit    | Status     | Effects                                            |
| ------ | ---------- | -------------------------------------------------- |
| `0x04` | Paralyzed? | Skips the character's turn                         |
| `0x08` | Blind      | Has a 50% chance of not calculating the attack     |
| `0x10` | Mute       | Cannot use certain abilities                       |
| `0x20` | Confused   | Cannot be controlled by the player                 |
| `0x40` | Sleeping   | Skips the character's turn, will eventually revert |
| `0x80` | Poisoned   | Drains (current HP + 5)/4 HP every turn            |
## Blind
If the attacker is blind, roll a random number and check if that number `& 2` is zero. If it is, then calculate the attack. Otherwise, the attack misses. The normal [[accuracy]] check happens if the attack is calculated.
```
801dc8f0 lhu    $v0, 0x5f10(at) ; load status
801dc8f4 nop 
801dc8f8 andi   $v0, 0x0008 ; check for blindness status
801dc8fc beqz   $v0, 0x801dc970
801dc900 sltiu  $v0, $v1, 0x0003

; if the attacker is blind
801dc904 jal    0x8017e3d4 ; call random number function
801dc908 nop    
8017e3d4 li     $t2, 0x00a0
8017e3d8 jr     $t2
8017e3dc li     $t1, 0x002f

801dc90c andi   $v0, 0x0002 ; random number & 2
801dc910 beqz   $v0, 0x801dc96c ; if the value of random number & 2 is 0, then the attack should be calculated
```
This code can be found at 
```
BIN/BATTLE/BATTLE.EMI: 0004ecf0
BIN/BATTLE/BATTLE2.EMI: 0004ecf0
BIN/BOSS/BOSS001.EMI: 0000c4f0
BIN/BOSS/BOSS002.EMI: 0004fcf0
BIN/BOSS/BOSS004.EMI: 0000c4f0
BIN/BOSS/BOSS007.EMI: 0004ecf0
BIN/BOSS/BOSS008.EMI: 0004ccf0
BIN/BOSS/BOSS012.EMI: 0004fcf0
BIN/BOSS/BOSS013.EMI: 0004fcf0
BIN/BOSS/BOSS014.EMI: 0004ecf0
BIN/BOSS/BOSS015.EMI: 0004ecf0
BIN/BOSS/BOSS017.EMI: 0004fcf0
BIN/BOSS/BOSS018.EMI: 0004fcf0
BIN/BOSS/BOSS019.EMI: 0004fcf0
BIN/BOSS/BOSS020.EMI: 0004fcf0
BIN/BOSS/BOSS021.EMI: 0004fcf0
BIN/BOSS/BOSS022.EMI: 0000c4f0
BIN/BOSS/BOSS023.EMI: 0004ccf0
BIN/BOSS/BOSS024.EMI: 0004fcf0
BIN/BOSS/BOSS025.EMI: 0000c4f0
BIN/BOSS/BOSS027.EMI: 0004fcf0
BIN/BOSS/BOSS028.EMI: 0004fcf0
BIN/BOSS/BOSS029.EMI: 0004fcf0
BIN/BOSS/BOSS030.EMI: 0004fcf0
BIN/BOSS/BOSS031.EMI: 0000c4f0
BIN/BOSS/BOSS032.EMI: 0004fcf0
BIN/BOSS/BOSS033.EMI: 0004ecf0
BIN/BOSS/BOSS034.EMI: 0004fcf0
BIN/BOSS/BOSS035.EMI: 0004fcf0
BIN/BOSS/BOSS036.EMI: 0004fcf0
BIN/BOSS/BOSS037.EMI: 0004fcf0
BIN/BOSS/BOSS038.EMI: 0004fcf0
BIN/BOSS/BOSS040.EMI: 0004fcf0
BIN/BOSS/BOSS042.EMI: 0004fcf0
BIN/BOSS/BOSS046.EMI: 0004fcf0
BIN/BOSS/BOSS047.EMI: 0004fcf0
BIN/BOSS/BOSS049.EMI: 0004fcf0
BIN/BOSS/BOSS050.EMI: 0004fcf0
BIN/BOSS/BOSS051.EMI: 0004fcf0
BIN/BOSS/BOSS052.EMI: 0004d4f0
BIN/BOSS/BOSS054.EMI: 0004fcf0
BIN/BOSS/BOSS055.EMI: 00052cf0
```
## Poisoned
### Battle
### Field
A poisoned party member loses 1 HP every ten steps:
```
801c3498 jal    0x8016813c ; go to the HP change function
801c349c li     $a0, 0x0001 ; load the HP change
...
801c34e4 li     $a1, 0x0001 ; load the number for the indicator
```
The code can be found at `BIN/ETC/GAME.EMI: 0002e498`
