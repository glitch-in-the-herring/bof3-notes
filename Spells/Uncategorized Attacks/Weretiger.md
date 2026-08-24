| Spell ID         | Targeting     | Power | AP  | Element | Battle Spell Call |
| ---------------- | ------------- | ----- | --- | ------- | ----------------- |
| `0x40`<br>64<br> | `0xe`<br>Self | 0<br> | 0   | None    | `0x4b`            |
Weretiger transforms Rei into an uncontrollable Weretiger for either the rest of the battle or until he is knocked out. If revived, he returns to normal.
Rei's PWR is multiplied by 3 in this mode:
```
800aa154 lhu    $v1, 0x5f24(at) ; load current PWR
800aa158 nop    
800aa15c sll    $v0, $v1, 0x01 ; multiply current PWR by 2
800aa160 addu   $v0, $v1 ; multiply current PWR by 3
800aa164 lui    $at, 0x8014
800aa168 addu   $at, $s1
800aa16c sh     $v0, 0x5f24(at) ; store new PWR
```
This code can be found at:
```
BIN/BATTLE/BATTLE.EMI: 0009d954
BIN/BATTLE/BATTLE2.EMI: 0009d954
BIN/BOSS/BOSS001.EMI: 0005b154
BIN/BOSS/BOSS002.EMI: 0009e954
BIN/BOSS/BOSS004.EMI: 0005b154
BIN/BOSS/BOSS007.EMI: 0009d954
BIN/BOSS/BOSS008.EMI: 0009b954
BIN/BOSS/BOSS012.EMI: 0009e954
BIN/BOSS/BOSS013.EMI: 0009e954
BIN/BOSS/BOSS014.EMI: 0009d954
BIN/BOSS/BOSS015.EMI: 0009d954
BIN/BOSS/BOSS017.EMI: 0009e954
BIN/BOSS/BOSS018.EMI: 0009e954
BIN/BOSS/BOSS019.EMI: 0009e954
BIN/BOSS/BOSS020.EMI: 0009e954
BIN/BOSS/BOSS021.EMI: 0009e954
BIN/BOSS/BOSS022.EMI: 0005b154
BIN/BOSS/BOSS023.EMI: 0009b954
BIN/BOSS/BOSS024.EMI: 0009e954
BIN/BOSS/BOSS025.EMI: 0005b154
BIN/BOSS/BOSS027.EMI: 0009e954
BIN/BOSS/BOSS028.EMI: 0009e954
BIN/BOSS/BOSS029.EMI: 0009e954
BIN/BOSS/BOSS030.EMI: 0009e954
BIN/BOSS/BOSS031.EMI: 0005b154
BIN/BOSS/BOSS032.EMI: 0009e954
BIN/BOSS/BOSS033.EMI: 0009d954
BIN/BOSS/BOSS034.EMI: 0009e954
BIN/BOSS/BOSS035.EMI: 0009e954
BIN/BOSS/BOSS036.EMI: 0009e954
BIN/BOSS/BOSS037.EMI: 0009e954
BIN/BOSS/BOSS038.EMI: 0009e954
BIN/BOSS/BOSS040.EMI: 0009e954
BIN/BOSS/BOSS042.EMI: 0009e954
BIN/BOSS/BOSS046.EMI: 0009e954
BIN/BOSS/BOSS047.EMI: 0009e954
BIN/BOSS/BOSS049.EMI: 0009e954
BIN/BOSS/BOSS050.EMI: 0009e954
BIN/BOSS/BOSS051.EMI: 0009e954
BIN/BOSS/BOSS052.EMI: 0009c154
BIN/BOSS/BOSS054.EMI: 0009e954
BIN/BOSS/BOSS055.EMI: 000a1954
```
Rei is made uncontrollable in this state:
```
801ef720 ori    $v0, 0x0001 ; load status for uncontrollable
801ef724 lui    $at, 0x8014
801ef728 addu   $at, $v1
801ef72c sw     $v0, 0x5fb8(at) ; store uncontrollable status
```
This code can be found at `BIN/BMAGIC/MAGIC064.EMI: 00017320`
At the start of every turn, it increments a counter that goes up to a maximum of 6. On every turn that it can attack, the Weretiger rolls a random number from 0 to 19. If this random number is bigger than the turn counter, then Weretiger will attack the enemy's party. If the counter is already six, then the counter is treated as if it were still 5. Otherwise, it will select one of its own party members as the target.

| Turn | $P(\text{Attacking the Enemy})$ | $P(\text{Attacking the Party})$ |
| ---- | ------------------------------- | ------------------------------- |
| 0*   | 100%                            | 0%                              |
| 1    | 95%                             | 5%                              |
| 2    | 90%                             | 10%                             |
| 3    | 85%                             | 15%                             |
| 4    | 80%                             | 20%                             |
| 5    | 75%                             | 25%                             |
| 6+   | 75%                             | 25%                             |
\* extra turn immediately after the transformation
```
800ab5ac lbu    $s0, 0x5fc6(at) ; load turn counter
800ab5b0 slti   $v1, 0x0006
800ab5b4 bnez   $v1, 0x800ab5c0
800ab5b8 nop    

; if the turn counter is less than 6
800ab5c0 jal    0x8017e3d4 ; go to random number function
800ab5c4 nop    
8017e3d4 li     $t2, 0x00a0
8017e3d8 jr     $t2
8017e3dc li     $t1, 0x002f
...
800ab5c8 lui    $v1, 0x6666
800ab5cc ori    $v1, 0x6667
800ab5d0 mult   $v0, $v1
800ab5d4 sra    $v1, $v0, 0x1f
800ab5d8 mfhi   $a1, $hi
800ab5dc sra    $a0, $a1, 0x03
800ab5e0 subu   $a0, $v1
800ab5e4 sll    $v1, $a0, 0x02
800ab5e8 addu   $v1, $a0
800ab5ec sll    $v1, 0x02
800ab5f0 subu   $v0, $v1 ; get a random number between 0 and 19
800ab5f4 sll    $v1, $s0, 0x18
800ab5f8 sra    $v1, 0x18
800ab5fc slt    $v0, $v1 
800ab600 beqz   $v0, 0x800ab62c
800ab604 li     $v0, 0x0001

; if the random number is greater than the counter, attack the enemy
800ab62c jal    0x8017e3d4
800ab630 nop    
```
This code can be found at:
```
BIN/BATTLE/BATTLE.EMI: 0009edac
BIN/BATTLE/BATTLE2.EMI: 0009edac
BIN/BOSS/BOSS001.EMI: 0005c5ac
BIN/BOSS/BOSS002.EMI: 0009fdac
BIN/BOSS/BOSS004.EMI: 0005c5ac
BIN/BOSS/BOSS007.EMI: 0009edac
BIN/BOSS/BOSS008.EMI: 0009cdac
BIN/BOSS/BOSS012.EMI: 0009fdac
BIN/BOSS/BOSS013.EMI: 0009fdac
BIN/BOSS/BOSS014.EMI: 0009edac
BIN/BOSS/BOSS015.EMI: 0009edac
BIN/BOSS/BOSS017.EMI: 0009fdac
BIN/BOSS/BOSS018.EMI: 0009fdac
BIN/BOSS/BOSS019.EMI: 0009fdac
BIN/BOSS/BOSS020.EMI: 0009fdac
BIN/BOSS/BOSS021.EMI: 0009fdac
BIN/BOSS/BOSS022.EMI: 0005c5ac
BIN/BOSS/BOSS023.EMI: 0009cdac
BIN/BOSS/BOSS024.EMI: 0009fdac
BIN/BOSS/BOSS025.EMI: 0005c5ac
BIN/BOSS/BOSS027.EMI: 0009fdac
BIN/BOSS/BOSS028.EMI: 0009fdac
BIN/BOSS/BOSS029.EMI: 0009fdac
BIN/BOSS/BOSS030.EMI: 0009fdac
BIN/BOSS/BOSS031.EMI: 0005c5ac
BIN/BOSS/BOSS032.EMI: 0009fdac
BIN/BOSS/BOSS033.EMI: 0009edac
BIN/BOSS/BOSS034.EMI: 0009fdac
BIN/BOSS/BOSS035.EMI: 0009fdac
BIN/BOSS/BOSS036.EMI: 0009fdac
BIN/BOSS/BOSS037.EMI: 0009fdac
BIN/BOSS/BOSS038.EMI: 0009fdac
BIN/BOSS/BOSS040.EMI: 0009fdac
BIN/BOSS/BOSS042.EMI: 0009fdac
BIN/BOSS/BOSS046.EMI: 0009fdac
BIN/BOSS/BOSS047.EMI: 0009fdac
BIN/BOSS/BOSS049.EMI: 0009fdac
BIN/BOSS/BOSS050.EMI: 0009fdac
BIN/BOSS/BOSS051.EMI: 0009fdac
BIN/BOSS/BOSS052.EMI: 0009d5ac
BIN/BOSS/BOSS054.EMI: 0009fdac
BIN/BOSS/BOSS055.EMI: 000a2dac
```
The code that increments the counter:
```
801d4da8 lbu    $v1, 0x5fc6(at) ; load current turn counter
801d4dac nop    
801d4db0 sltiu  $v0, $v1, 0x0006 ; check if less than 6
801d4db4 beqz   $v0, 0x801d4dc4
801d4db8 addiu  $v1, 0x0001 ; increment

; if less than 6
801d4dbc addu   $v0, $a0, $s2
801d4dc0 sb     $v1, 0x0136(v0) ; store turn counter
```
Can be found at:
```
BIN/BATTLE/BATTLE.EMI: 000471a8
BIN/BATTLE/BATTLE2.EMI: 000471a8
BIN/BOSS/BOSS001.EMI: 000049a8
BIN/BOSS/BOSS002.EMI: 000481a8
BIN/BOSS/BOSS004.EMI: 000049a8
BIN/BOSS/BOSS007.EMI: 000471a8
BIN/BOSS/BOSS008.EMI: 000451a8
BIN/BOSS/BOSS012.EMI: 000481a8
BIN/BOSS/BOSS013.EMI: 000481a8
BIN/BOSS/BOSS014.EMI: 000471a8
BIN/BOSS/BOSS015.EMI: 000471a8
BIN/BOSS/BOSS017.EMI: 000481a8
BIN/BOSS/BOSS018.EMI: 000481a8
BIN/BOSS/BOSS019.EMI: 000481a8
BIN/BOSS/BOSS020.EMI: 000481a8
BIN/BOSS/BOSS021.EMI: 000481a8
BIN/BOSS/BOSS022.EMI: 000049a8
BIN/BOSS/BOSS023.EMI: 000451a8
BIN/BOSS/BOSS024.EMI: 000481a8
BIN/BOSS/BOSS025.EMI: 000049a8
BIN/BOSS/BOSS027.EMI: 000481a8
BIN/BOSS/BOSS028.EMI: 000481a8
BIN/BOSS/BOSS029.EMI: 000481a8
BIN/BOSS/BOSS030.EMI: 000481a8
BIN/BOSS/BOSS031.EMI: 000049a8
BIN/BOSS/BOSS032.EMI: 000481a8
BIN/BOSS/BOSS033.EMI: 000471a8
BIN/BOSS/BOSS034.EMI: 000481a8
BIN/BOSS/BOSS035.EMI: 000481a8
BIN/BOSS/BOSS036.EMI: 000481a8
BIN/BOSS/BOSS037.EMI: 000481a8
BIN/BOSS/BOSS038.EMI: 000481a8
BIN/BOSS/BOSS040.EMI: 000481a8
BIN/BOSS/BOSS042.EMI: 000481a8
BIN/BOSS/BOSS046.EMI: 000481a8
BIN/BOSS/BOSS047.EMI: 000481a8
BIN/BOSS/BOSS049.EMI: 000481a8
BIN/BOSS/BOSS050.EMI: 000481a8
BIN/BOSS/BOSS051.EMI: 000481a8
BIN/BOSS/BOSS052.EMI: 000459a8
BIN/BOSS/BOSS054.EMI: 000481a8
BIN/BOSS/BOSS055.EMI: 0004b1a8
```