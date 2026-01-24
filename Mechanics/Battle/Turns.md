The index of the current active combatant in the current active turn is located at:
* `0x80146374` in the RAM
The queue of the combatants is located at:
* `0x8014630c` in the RAM
The priority queue of the combatants is located at:
* `0x801eb550` in the RAM
There are 11 possible combatant slot (3 player + 8 max enemies). An index of `ff` means that there are no combatants in this slot. Duplicating an index does not produce any effects. Assigning an inactive index (e.g. assigning one of the enemy indices during an extra turn) does not produce any effects.
## Queue Ordering
To determine the order of the combatants during a turn, the game assigns priorities to each combatant. Combatants with larger priority values will be assigned to the front of the queue. For the player's party member, this weight is calculated as so:
$$
w = p + SPD
$$
$$
p = \left\lfloor \frac{Ma}{100} \right\rfloor
$$
$$
a = \begin{cases}
4 & \text{Heal spell with 0 learning difficulty}\\
2 & \text{Assist spell with 0 learning difficulty}\\
2 & \text{Skill with 0 learning difficulty}\\
0 & \text{Otherwise}
\end{cases}
%\begin{cases}
%0 & \mathrm{Examine}\\
%1 & \mathrm{Attack}\\
%2 & \mathrm{Defend}\\
%4 & \mathrm{Spell}\\
%5 & \mathrm{Item}
%\end{cases}
$$
$$
M = \begin{cases}
100 &  0 \leq L < 8\\
125 & 8 \leq L < 16\\
150 & 16 \leq L < 32 \\
200 & 32 \leq L < 48 \\
250 & 48 \leq L \leq 99
\end{cases}
$$
Where:
* $L$ is the combatant's level
The code can be found in the following locations:
```
BIN/BATTLE/BATTLE.EMI: 0004cf0c
BIN/BATTLE/BATTLE2.EMI: 0004cf0c
BIN/BOSS/BOSS001.EMI: 0000a70c
BIN/BOSS/BOSS002.EMI: 0004df0c
BIN/BOSS/BOSS004.EMI: 0000a70c
BIN/BOSS/BOSS007.EMI: 0004cf0c
BIN/BOSS/BOSS008.EMI: 0004af0c
BIN/BOSS/BOSS012.EMI: 0004df0c
BIN/BOSS/BOSS013.EMI: 0004df0c
BIN/BOSS/BOSS014.EMI: 0004cf0c
BIN/BOSS/BOSS015.EMI: 0004cf0c
BIN/BOSS/BOSS017.EMI: 0004df0c
BIN/BOSS/BOSS018.EMI: 0004df0c
BIN/BOSS/BOSS019.EMI: 0004df0c
BIN/BOSS/BOSS020.EMI: 0004df0c
BIN/BOSS/BOSS021.EMI: 0004df0c
BIN/BOSS/BOSS022.EMI: 0000a70c
BIN/BOSS/BOSS023.EMI: 0004af0c
BIN/BOSS/BOSS024.EMI: 0004df0c
BIN/BOSS/BOSS025.EMI: 0000a70c
BIN/BOSS/BOSS027.EMI: 0004df0c
BIN/BOSS/BOSS028.EMI: 0004df0c
BIN/BOSS/BOSS029.EMI: 0004df0c
BIN/BOSS/BOSS030.EMI: 0004df0c
BIN/BOSS/BOSS031.EMI: 0000a70c
BIN/BOSS/BOSS032.EMI: 0004df0c
BIN/BOSS/BOSS033.EMI: 0004cf0c
BIN/BOSS/BOSS034.EMI: 0004df0c
BIN/BOSS/BOSS035.EMI: 0004df0c
BIN/BOSS/BOSS036.EMI: 0004df0c
BIN/BOSS/BOSS037.EMI: 0004df0c
BIN/BOSS/BOSS038.EMI: 0004df0c
BIN/BOSS/BOSS040.EMI: 0004df0c
BIN/BOSS/BOSS042.EMI: 0004df0c
BIN/BOSS/BOSS046.EMI: 0004df0c
BIN/BOSS/BOSS047.EMI: 0004df0c
BIN/BOSS/BOSS049.EMI: 0004df0c
BIN/BOSS/BOSS050.EMI: 0004df0c
BIN/BOSS/BOSS051.EMI: 0004df0c
BIN/BOSS/BOSS052.EMI: 0004b70c
BIN/BOSS/BOSS054.EMI: 0004df0c
BIN/BOSS/BOSS055.EMI: 00050f0c
```

```
801dab98 li     $s4, 0x0004 ; load the action ID for casting spells
801dab9c move   $s2, $r0
801daba0 move   $s3, $r0
801daba4 li     $s1, 0x0001
801daba8 lui    $v0, 0x8014
801dabac lbu    $v0, 0x63ba(v0)
801dabb0 nop    
801dabb4 beqz   $v0, 0x801dabe4
801dabb8 andi   $v0, $s3, 0x00ff
801dabbc sll    $v1, $v0, 0x02
801dabc0 addu   $v1, $v0
801dabc4 sll    $v1, 0x06
801dabc8 lui    $at, 0x8014
801dabcc addu   $at, $v1
801dabd0 lw     $v0, 0x5fb8(at)
801dabd4 nop    
801dabd8 andi   $v0, 0x8000
801dabdc beqz   $v0, 0x801dad9c
801dabe0 nop    
801dabe4 andi   $s0, $s3, 0x00ff
801dabe8 jal    0x801db9e4
801dabec move   $a0, $s0
801db9e4 andi   $v1, $a0, 0x00ff
801db9e8 sltiu  $v0, $v1, 0x0003
801db9ec beqz   $v0, 0x801dba74
801db9f0 sll    $v0, $v1, 0x02
801db9f4 addu   $v0, $v1
801db9f8 sll    $v1, $v0, 0x06
801db9fc lui    $at, 0x8014
801dba00 addu   $at, $v1
801dba04 lbu    $v0, 0x5e90(at)
801dba08 nop    
801dba0c andi   $v0, 0x0001
801dba10 beqz   $v0, 0x801dbb18
801dba14 move   $v0, $r0
801dba18 lui    $at, 0x8014
801dba1c addu   $at, $v1
801dba20 lhu    $v0, 0x5f10(at)
801dba24 nop    
801dba28 andi   $v0, 0x4944
801dba2c bnez   $v0, 0x801dbb18
801dba30 move   $v0, $r0
801dba34 lui    $v0, 0x8014
801dba38 lbu    $v0, 0x63ce(v0)
801dba3c nop    
801dba40 beqz   $v0, 0x801dba64
801dba44 nop    
801dba64 lui    $v1, 0x8014
801dba68 lbu    $v1, 0x6324(v1)
801dba6c j      0x801dbb04
801dba70 li     $v0, 0x0002
801dbb04 beq    $v1, $v0, 0x801dbb14
801dbb08 li     $v0, 0x0003
801dbb0c bne    $v1, $v0, 0x801dbb18
801dbb10 li     $v0, 0x0001
801dbb18 jr     $ra
801dbb1c nop    
801dabf0 andi   $v0, 0x00ff
801dabf4 beqz   $v0, 0x801dad9c
801dabf8 andi   $v0, $s2, 0x00ff
801dabfc sll    $a0, $v0, 0x02
801dac00 andi   $v0, $s3, 0x00ff
801dac04 lui    $at, 0x801f
801dac08 addu   $at, $a0
801dac0c sh     $v0, -0x4aae(at)
801dac10 sll    $v0, $s0, 0x02
801dac14 addu   $v0, $s0
801dac18 sll    $v1, $v0, 0x06
801dac1c lui    $at, 0x801f
801dac20 addu   $at, $a0
801dac24 sh     $r0, -0x4ab0(at)
801dac28 lui    $at, 0x8014
801dac2c addu   $at, $v1
801dac30 lbu    $v0, 0x5fa9(at) ; current action of the character
801dac34 nop    
801dac38 bne    $v0, $s4, 0x801daccc 
801dac3c nop    

; If the current action is casting a spell
801dac40 lui    $at, 0x8014
801dac44 addu   $at, $v1
801dac48 lhu    $v1, 0x5faa(at) ; load current spell
801dac4c nop    
801dac50 sll    $v0, $v1, 0x02
801dac54 addu   $v0, $v1
801dac58 sll    $v0, 0x02
801dac5c lui    $at, 0x801d
801dac60 addu   $at, $v0
801dac64 lbu    $v1, -0x58e7(at) ; load current spell's category and difficulty
801dac68 nop    
801dac6c beq    $v1, $s1, 0x801dacb4
801dac70 slti   $v0, $v1, 0x0002
801dac74 beqz   $v0, 0x801dac8c
801dac78 nop    
801dac7c beqz   $v1, 0x801daca0
801dac80 andi   $v1, $s3, 0x00ff
801daca0 lui    $at, 0x801f
801daca4 addu   $at, $a0
801daca8 sh     $s4, -0x4ab0(at)
801dacac j      0x801dacd0
801dacb0 nop    
801dacd0 sll    $v0, $v1, 0x02 
801dacd4 addu   $v0, $v1
801dacd8 sll    $s0, $v0, 0x06
801dacdc lui    $at, 0x8014
801dace0 addu   $at, $s0
801dace4 lbu    $v1, 0x5fa9(at)
801dace8 li     $v0, 0x0005
801dacec bne    $v1, $v0, 0x801dad04
801dacf0 andi   $v0, $s2, 0x00ff
801dad04 lui    $at, 0x8014
801dad08 addu   $at, $s0
801dad0c lbu    $a0, 0x5f0a(at) ; load combatant's level
801dad10 jal    0x801db434
801dad14 li     $a1, 0x0001
801db434 move   $a2, $r0 ; set multiplier index to 0
801db438 andi   $a1, 0x00ff
801db43c lui    $v1, 0x801f
801db440 addiu  $v1, -0x5078
801db444 sll    $v0, $a1, 0x01
801db448 addu   $v0, $a1
801db44c sll    $v0, 0x01
801db450 addu   $a1, $v0, $v1
801db454 andi   $a0, 0x00ff
801db458 andi   $v1, $a2, 0x00ff

    ; Loop the following until the level threshold is greater than the combatant's level
    801db45c addu   $v0, $a1, $v1
    801db460 lbu    $v0, 0x0000(v0) ; load the current threshold
    801db464 nop    
    801db468 sltu   $v0, $a0, $v0
    801db46c bnez   $v0, 0x801db48c
    801db470 move   $v0, $v1

    ; if the combatant's level is greater than the threshold
    801db474 addiu  $a2, 0x0001 ; increment multiplier index
    801db478 andi   $v0, $a2, 0x00ff
    801db47c sltiu  $v0, 0x0006
    801db480 bnez   $v0, 0x801db45c ; loop for at most six times
    801db484 andi   $v1, $a2, 0x00ff

801db46c bnez   $v0, 0x801db48c
801db470 move   $v0, $v1 ; move multiplier index to v0
801db48c jr     $ra
801db490 nop    
801dad18 andi   $a1, $s2, 0x00ff
801dad1c sll    $a1, 0x02
801dad20 andi   $v0, 0x00ff
801dad24 sll    $v0, 0x01
801dad28 lui    $at, 0x801f
801dad2c addu   $at, $a1
801dad30 lh     v1, -0x4ab0(at) ; action id, let this be a
801dad34 lui    $at, 0x801f
801dad38 addu   $at, $v0
801dad3c lhu    $v0, -0x50c4(at) ; get the multiplier from the multiplier index
801dad40 nop    
801dad44 mult   $v1, $v0 ; multiply a by the multiplier
801dad48 lui    $a0, 0x51eb
801dad4c ori    $a0, 0x851f
801dad50 mflo   $t4, $lo
801dad54 sll    $v1, $t4, 0x10
801dad58 sra    $v0, $v1, 0x10
801dad5c mult   $v0, $a0
801dad60 sra    $v1, 0x1f
801dad64 mfhi   $t4, $hi ; divide M*a by 100, let this be p
801dad68 sra    $v0, $t4, 0x05
801dad6c subu   $v0, $v1
801dad70 lui    $at, 0x801f
801dad74 addu   $at, $a1
801dad78 sh     $v0, -0x4ab0(at)
801dad7c lui    $at, 0x8014
801dad80 addu   $at, $s0
801dad84 lhu    $v1, 0x5f28(at) ; add combatant's speed to p
801dad88 addiu  $s2, 0x0001
801dad8c addu   $v0, $v1 ; add speed
801dad90 lui    $at, 0x801f
801dad94 addu   $at, $a1
801dad98 sh     $v0, -0x4ab0(at) ; final priority score
```
## Extra Turns
If a party member's AGL is greater than twice the average AGL of the enemy party, then the party member gets an extra turn.