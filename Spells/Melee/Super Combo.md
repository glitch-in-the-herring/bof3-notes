| Spell ID   | Targeting                              | Power | AP  | Element | Battle Spell Call |
| ---------- | -------------------------------------- | ----- | --- | ------- | ----------------- |
| `0x3`<br>3 | `0x6a`<br>Single<br>Always enemy party | 0     | 12  | None    | `0x67`            |
Super Combo shows a sequence of buttons that the player must press successfully in order to increase the combo counter. Once the player hits the wrong button, then the sequence ends and the attack is dealt to the target.
Data for the spell is stored at `0x801ec860`:

| Position | Description     |
| -------- | --------------- |
| 0        |                 |
| 1        | Countdown Timer |
| 2        | Number of hits  |
| 3        | Button ID       |
The Button IDs are:

| ID  | Button   |
| --- | -------- |
| 0   | Circle   |
| 1   | Cross    |
| 2   | Triangle |
| 3   | Square   |
The game selects a button for the player to press and then starts the countdown timer. The countdown timer's duration depends on the number of hits the player has successfully landed so far:

| Hits | Counter | Actual duration <br>(assuming 60 FPS) |
| ---- | ------- | ------------------------------------- |
| 0    | 60      | 2 seconds                             |
| 1    | 45      | 1.5 seconds                           |
| 2    | 30      | 1 second                              |
| 3    | 25      | 0.83 seconds                          |
| 4    | 20      | 0.67 seconds                          |
| 5    | 18      | 0.6 seconds                           |
| 6    | 16      | 0.53 seconds                          |
| 7    | 14      | 0.467 seconds                         |
| 8    | 12      | 0.4 seconds                           |
| 9    | 10      | 0.33 seconds                          |
| 10   | 9       | 0.3 seconds                           |
| 11   | 8       | 0.267 seconds                         |
| 12   | 7       | 0.23 seconds                          |
| 13   | 6       | 0.2 seconds                           |
| 14   | 5       | 0.167 seconds                         |
| 15   | 4       | 0.13 seconds                          |
| 16+  | 3       | 0.1 seconds                           |
Once the button is pressed, the timer is reset to six counts before rolling for the next button. 
```
801eeed0 jal    0x8017e3d4 ; call random number function
801eeed4 nop    
8017e3d4 li     $t2, 0x00a0
8017e3d8 jr     $t2
...
801eeed8 lui    $v1, 0x1f80
801eeedc lw     $v1, 0x0044(v1)
801eeee0 andi   $v0, 0x0003 ; get random number from 0 to  3
801eeee4 sb     $v0, 0x000b(v1) ; store new button 
801eeee8 lui    $v1, 0x1f80
801eeeec lw     $v1, 0x0044(v1)
801eeef0 nop    
801eeef4 lbu    $a0, 0x000a(v1) ; load current number of hits
801eeef8 nop    
801eeefc sltiu  $v0, $a0, 0x0010
801eef00 beqz   $v0, 0x801eef1c

; if the current combo hits is more than 16
801eef04 li     $v0, 0x0003 ; set countdown amount to 3
801eef08 lui    $at, 0x801f
801eef0c addu   $at, $a0
801eef10 lbu    $v0, 0x0a84(at) ; load countdown amount
801eef14 j      0x801eef20
801eef18 sb     $v0, 0x0009(v1) ; store countdown amount
```
This code can be found at `BIN/BMAGIC/MAGIC003.EMI: 00012ad0`
After the player breaks the sequence, the attack animation is displayed and the damage is calculated. The damage is calculated by looping the [[Melee Formula]] for (combo hit - 1) times.
```
800a0d00 lbu    $v1, 0x0062(s3) ; load combo counter 
800a0d04 andi   $v0, $s2, 0x00ff
800a0d08 sltu   $v0, $v1 ; check if the counter is less than combo counter
800a0d0c bnez   $v0, 0x800a0ca4
800a0d10 andi   $v1, $s2, 0x00ff
800a0ca4 sltiu  $v0, $v1, 0x0007
800a0ca8 beqz   $v0, 0x800a0cbc

; if the current loop counter is not less than 7
800a0cac li     $s0, 0x0003 ; set the loop multiplier to 3

800a0cb0 lui    $at, 0x800b
800a0cb4 addu   $at, $v1
800a0cb8 lb     $s0, 0x4924(at) ; load multiplier for the current loop
800a0cbc lbu    $a0, 0x0000(s3)
800a0cc0 lbu    $a1, 0x0020(s3) ; load target index
800a0cc4 jal    0x801dc044 ; call melee function
800a0cc8 li     $a2, 0xffff
...
800a0ccc sll    $v0, 0x10
800a0cd0 sra    $v0, 0x10
800a0cd4 mult   $v0, $s0 ; multiply damage formula results by loop multiplier, let this be the scaled damage
800a0cd8 mflo   $v0, $lo
800a0cdc lui    $v1, 0x6666
800a0ce0 ori    $v1, 0x6667
800a0ce4 mult   $v0, $v1 ;
800a0ce8 addiu  $s2, 0x0001
800a0cec sra    $v0, 0x1f
800a0cf0 mfhi   $a3, $hi
800a0cf4 sra    $v1, $a3, 0x02 ; divide scaled damaged by 10
800a0cf8 subu   $v0, $v1, $v0
800a0cfc addu   $s1, $v0 ; add scaled damage to total damage
```
The code can be found at:
```
BIN/BATTLE/BATTLE.EMI: 00094500
BIN/BATTLE/BATTLE2.EMI: 00094500
BIN/BOSS/BOSS001.EMI: 00051d00
BIN/BOSS/BOSS002.EMI: 00095500
BIN/BOSS/BOSS004.EMI: 00051d00
BIN/BOSS/BOSS007.EMI: 00094500
BIN/BOSS/BOSS008.EMI: 00092500
BIN/BOSS/BOSS012.EMI: 00095500
BIN/BOSS/BOSS013.EMI: 00095500
BIN/BOSS/BOSS014.EMI: 00094500
BIN/BOSS/BOSS015.EMI: 00094500
BIN/BOSS/BOSS017.EMI: 00095500
BIN/BOSS/BOSS018.EMI: 00095500
BIN/BOSS/BOSS019.EMI: 00095500
BIN/BOSS/BOSS020.EMI: 00095500
BIN/BOSS/BOSS021.EMI: 00095500
BIN/BOSS/BOSS022.EMI: 00051d00
BIN/BOSS/BOSS023.EMI: 00092500
BIN/BOSS/BOSS024.EMI: 00095500
BIN/BOSS/BOSS025.EMI: 00051d00
BIN/BOSS/BOSS027.EMI: 00095500
BIN/BOSS/BOSS028.EMI: 00095500
BIN/BOSS/BOSS029.EMI: 00095500
BIN/BOSS/BOSS030.EMI: 00095500
BIN/BOSS/BOSS031.EMI: 00051d00
BIN/BOSS/BOSS032.EMI: 00095500
BIN/BOSS/BOSS033.EMI: 00094500
BIN/BOSS/BOSS034.EMI: 00095500
BIN/BOSS/BOSS035.EMI: 00095500
BIN/BOSS/BOSS036.EMI: 00095500
BIN/BOSS/BOSS037.EMI: 00095500
BIN/BOSS/BOSS038.EMI: 00095500
BIN/BOSS/BOSS040.EMI: 00095500
BIN/BOSS/BOSS042.EMI: 00095500
BIN/BOSS/BOSS046.EMI: 00095500
BIN/BOSS/BOSS047.EMI: 00095500
BIN/BOSS/BOSS049.EMI: 00095500
BIN/BOSS/BOSS050.EMI: 00095500
BIN/BOSS/BOSS051.EMI: 00095500
BIN/BOSS/BOSS052.EMI: 00092d00
BIN/BOSS/BOSS054.EMI: 00095500
BIN/BOSS/BOSS055.EMI: 00098500
```

The loop multiplier depends on the current loop counter:

| Counter | Multiplier |
| ------- | ---------- |
| 0       | 5          |
| 1       | 5          |
| 2       | 5          |
| 3       | 5          |
| 4       | 4          |
| 5       | 4          |
| 6       | 4          |
| 7+      | 3          |
This table can be found at:
```
BIN/BATTLE/BATTLE.EMI: 000a8124
BIN/BATTLE/BATTLE2.EMI: 000a8124
BIN/BOSS/BOSS001.EMI: 00065924
BIN/BOSS/BOSS002.EMI: 000a9124
BIN/BOSS/BOSS004.EMI: 00065924
BIN/BOSS/BOSS007.EMI: 000a8124
BIN/BOSS/BOSS008.EMI: 000a6124
BIN/BOSS/BOSS012.EMI: 000a9124
BIN/BOSS/BOSS013.EMI: 000a9124
BIN/BOSS/BOSS014.EMI: 000a8124
BIN/BOSS/BOSS015.EMI: 000a8124
BIN/BOSS/BOSS017.EMI: 000a9124
BIN/BOSS/BOSS018.EMI: 000a9124
BIN/BOSS/BOSS019.EMI: 000a9124
BIN/BOSS/BOSS020.EMI: 000a9124
BIN/BOSS/BOSS021.EMI: 000a9124
BIN/BOSS/BOSS022.EMI: 00065924
BIN/BOSS/BOSS023.EMI: 000a6124
BIN/BOSS/BOSS024.EMI: 000a9124
BIN/BOSS/BOSS025.EMI: 00065924
BIN/BOSS/BOSS027.EMI: 000a9124
BIN/BOSS/BOSS028.EMI: 000a9124
BIN/BOSS/BOSS029.EMI: 000a9124
BIN/BOSS/BOSS030.EMI: 000a9124
BIN/BOSS/BOSS031.EMI: 00065924
BIN/BOSS/BOSS032.EMI: 000a9124
BIN/BOSS/BOSS033.EMI: 000a8124
BIN/BOSS/BOSS034.EMI: 000a9124
BIN/BOSS/BOSS035.EMI: 000a9124
BIN/BOSS/BOSS036.EMI: 000a9124
BIN/BOSS/BOSS037.EMI: 000a9124
BIN/BOSS/BOSS038.EMI: 000a9124
BIN/BOSS/BOSS040.EMI: 000a9124
BIN/BOSS/BOSS042.EMI: 000a9124
BIN/BOSS/BOSS046.EMI: 000a9124
BIN/BOSS/BOSS047.EMI: 000a9124
BIN/BOSS/BOSS049.EMI: 000a9124
BIN/BOSS/BOSS050.EMI: 000a9124
BIN/BOSS/BOSS051.EMI: 000a9124
BIN/BOSS/BOSS052.EMI: 000a6924
BIN/BOSS/BOSS054.EMI: 000a9124
BIN/BOSS/BOSS055.EMI: 000ac124
```

