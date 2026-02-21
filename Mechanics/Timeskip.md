## Angel Tower
This timeskip happens after you defeat Garr at the Angel Tower. In the transition from the scene where Ryu (as a whelp) walks around in the darkness to the scene where Ryu (still as a whelp) walks around in Dauna Mine, Ryu and Nina's stats are changed:

```
801faea4 sb     $s0, 0x496d(at) ; store Ryu's new character ID
801faea8 lbu    $v1, 0x0000(a0)
801faeac nop    
801faeb0 sll    $v0, $v1, 0x02
801faeb4 addu   $v0, $v1
801faeb8 sll    $v0, 0x03
801faebc addu   $v0, $v1
801faec0 sll    $v0, 0x02
801faec4 li     $v1, 0x0037
801faec8 lui    $at, 0x8014
801faecc addu   $at, $v0
801faed0 sb     $v1, 0x49bc(at) ; store Ryu's new surprise
801faed4 lbu    $v1, 0x0000(a0)
801faed8 li     $a1, 0x0008
801faedc sll    $v0, $v1, 0x02
801faee0 addu   $v0, $v1
801faee4 sll    $v0, 0x03
801faee8 addu   $v0, $v1
801faeec sll    $v0, 0x02
801faef0 lui    $at, 0x8014
801faef4 addu   $at, $v0
801faef8 sb     $a1, 0x49bf(at) ; store Ryu's new dodge
801faefc lbu    $v1, 0x0000(a0)
801faf00 nop    
801faf04 sll    $v0, $v1, 0x02
801faf08 addu   $v0, $v1
801faf0c sll    $v0, 0x03
801faf10 addu   $v0, $v1
801faf14 sll    $v0, 0x02
801faf18 li     $v1, 0x0064
801faf1c lui    $at, 0x8014
801faf20 addu   $at, $v0
801faf24 sb     $v1, 0x49c0(at) ; store Ryu's new accuracy
801faf28 lui    $v1, 0x8018
801faf2c lbu    $v1, 0x1b18(v1)
801faf30 nop    
801faf34 sll    $v0, $v1, 0x02
801faf38 addu   $v0, $v1
801faf3c sll    $v0, 0x03
801faf40 addu   $v0, $v1
801faf44 sll    $v0, 0x02
801faf48 lui    $at, 0x8014
801faf4c addu   $at, $v0
801faf50 sb     $a1, 0x496d(at) ; store Nina's new character ID
801faf54 lui    $v1, 0x8018
801faf58 lbu    $v1, 0x1b18(v1)
801faf5c nop    
801faf60 sll    $v0, $v1, 0x02
801faf64 addu   $v0, $v1
801faf68 sll    $v0, 0x03
801faf6c addu   $v0, $v1
801faf70 sll    $v0, 0x02
801faf74 li     $v1, 0x000c
801faf78 lui    $at, 0x8014
801faf7c addu   $at, $v0
801faf80 sb     $v1, 0x49bf(at) ; store Nina's new dodge
```
This code can be found at `BIN/SCENARIO/SCENA08.EMI: 00004aa4`
## Rei
This timeskip happens when the party selection screen appears after Mikba knocks Rei unconscious. The game adds a fixed 10,000 EXP to Rei and then iterates through the level up table to give new stats to Rei
```
801fdf98 lw     $v0, 0x0000(s0) ; load Rei's current EXP
801fdf9c li     $a0, 0x0004
801fdfa0 addiu  $v0, 0x2710  ; add 10,000 to Rei's EXP
801fdfa4 jal    0x801addd4
801fdfa8 sw     $v0, 0x0000(s0) ; store Rei's new EXP
```
This code can be found at `BIN/SCENARIO/SCENA08.EMI: 00007b98`.
Rei then gains the Weretiger ability either during the fight with Mikba, if he is revived during the battle, or after the fight, if he was never revived.
If Rei is revived mid-battle, these lines are executed:
```
800c1fa0 li     $a0, 0x0040 ; load spell ID for field data
...
800c1fd4 li     $v1, 0x0040 ; load spell ID for casting
...
800c2000 li     $a0, 0x0040 ; load spell ID for battle data
```
The code can be found at `BIN/BOSS/BOSS034.EMI: 000ac7a0`
If Rei was never revived mid-battle, these lines are executed instead:
```
800c224c li     $a0, 0x0040 ; load spell ID for field data
...
800c2260 li     $a0, 0x0040 ; load spell ID for battle data
```
The code can be found at `BIN/BOSS/BOSS034.EMI: 000aca4c`
For some reason the game insists on adding the spell in the battle data, even though the battle is already over.