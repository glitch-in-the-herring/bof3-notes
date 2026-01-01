## Learning roll

When a character uses Examine on a specific enemy, they can learn skills used by that enemy.
The success rate of this mechanic is determined by:
$$
r = \mathrm{random}(0, 32767) \mod n 
$$
$$
\begin{cases}
\mathrm{success} & r = 0\\
\mathrm{fail} & r \neq 0
\end{cases}
$$
where $n$ is determined by the difficulty of the spell:

| Difficulty | $n$ | Probability |
| ---------- | --- | ----------- |
| 0          | 1   | 100%        |
| 1          | 2   | 50%         |
| 2          | 4   | 25%         |
| 3          | 8   | 12.5%       |
| 4          | 12  | 8.33%       |
| 5          | 16  | 6.25%       |
| 6          | 24  | 4.167%      |
| 7          | 48  | 2.083%      |
This table can be found at:
* `0x800b50dc` in the RAM
* In the following locations in the file:
```
BIN/BATTLE/BATTLE.EMI: 000a88dc
BIN/BATTLE/BATTLE2.EMI: 000a88dc
BIN/BOSS/BOSS001.EMI: 000660dc
BIN/BOSS/BOSS002.EMI: 000a98dc
BIN/BOSS/BOSS004.EMI: 000660dc
BIN/BOSS/BOSS007.EMI: 000a88dc
BIN/BOSS/BOSS008.EMI: 000a68dc
BIN/BOSS/BOSS012.EMI: 000a98dc
BIN/BOSS/BOSS013.EMI: 000a98dc
BIN/BOSS/BOSS014.EMI: 000a88dc
BIN/BOSS/BOSS015.EMI: 000a88dc
BIN/BOSS/BOSS017.EMI: 000a98dc
BIN/BOSS/BOSS018.EMI: 000a98dc
BIN/BOSS/BOSS019.EMI: 000a98dc
BIN/BOSS/BOSS020.EMI: 000a98dc
BIN/BOSS/BOSS021.EMI: 000a98dc
BIN/BOSS/BOSS022.EMI: 000660dc
BIN/BOSS/BOSS023.EMI: 000a68dc
BIN/BOSS/BOSS024.EMI: 000a98dc
BIN/BOSS/BOSS025.EMI: 000660dc
BIN/BOSS/BOSS027.EMI: 000a98dc
BIN/BOSS/BOSS028.EMI: 000a98dc
BIN/BOSS/BOSS029.EMI: 000a98dc
BIN/BOSS/BOSS030.EMI: 000a98dc
BIN/BOSS/BOSS031.EMI: 000660dc
BIN/BOSS/BOSS032.EMI: 000a98dc
BIN/BOSS/BOSS033.EMI: 000a88dc
BIN/BOSS/BOSS034.EMI: 000a98dc
BIN/BOSS/BOSS035.EMI: 000a98dc
BIN/BOSS/BOSS036.EMI: 000a98dc
BIN/BOSS/BOSS037.EMI: 000a98dc
BIN/BOSS/BOSS038.EMI: 000a98dc
BIN/BOSS/BOSS040.EMI: 000a98dc
BIN/BOSS/BOSS042.EMI: 000a98dc
BIN/BOSS/BOSS046.EMI: 000a98dc
BIN/BOSS/BOSS047.EMI: 000a98dc
BIN/BOSS/BOSS049.EMI: 000a98dc
BIN/BOSS/BOSS050.EMI: 000a98dc
BIN/BOSS/BOSS051.EMI: 000a98dc
BIN/BOSS/BOSS052.EMI: 000a70dc
BIN/BOSS/BOSS054.EMI: 000a98dc
BIN/BOSS/BOSS055.EMI: 000ac8dc
```
When the roll is successful, the game toggles the `0x08` bit of the `+0x124`-th bit from the start of the character's battle data. This marks that the character is the one. This only happens once, which means that only one character can learn a skill. If set this bit manually for multiple characters, only the first one will learn the spell, even though multiple messages will appear for each character with this bit active.
```
800aa6cc lhu    $v1, 0x0002(v0) ; load current spell
800aa6d0 nop    
800aa6d4 sll    $v0, $v1, 0x02
800aa6d8 addu   $v0, $v1
800aa6dc sll    $v0, 0x02
800aa6e0 lui    $at, 0x801d
800aa6e4 addu   $at, $v0
800aa6e8 lbu    $v0, -0x58e7(at) ; load spell learning flags
800aa6ec nop    
800aa6f0 srl    $v0, 0x04 ; isolate spell difficulty
800aa6f4 lui    $at, 0x800b
800aa6f8 addu   $at, $v0 ; add the difficulty as an offset to a base address
800aa6fc lbu    $s0, 0x50dc(at) ; load max dice roll, let this be d
800aa700 j      0x800aa748
800aa704 nop    
800aa748 jal    08017e3d4 ; call the rand() function
800aa74c nop     
...
800aa750 div    $v0, $s0 
800aa754 bnez   $s0, 0x800aa760
800aa758 nop    
800aa760 li     $at, -0x0001
800aa764 bne    $s0, $at, 0x800aa778
800aa768 lui    $at, 0x8000
800aa778 mfhi   $v0, $hi ; generate a random number between 0 and d-1 inclusive, let this be r+
800aa77c nop    
800aa780 andi   $v0, 0x00ff
800aa784 sltiu  $v0, 0x0001
800aa788 lw     $ra, 0x0018(sp)
800aa78c lw     $s1, 0x0014(sp)
800aa790 lw     $s0, 0x0010(sp)
800aa794 addiu  $sp, 0x0020
800aa798 jr     $ra
800aa79c nop    
800aa3e0 andi   $v0, 0x00ff
800aa3e4 bnez   $v0, 0x800aa408 
800aa3e8 andi   $v0, $s1, 0x00ff

; if r is zero, then the character can learn the spell
800aa408 addu   $v0, $s2, $v0
800aa40c sb     $s0, 0x0000(v0)
800aa410 addiu  $s1, 0x0001 ; add 1 to the  learner count??
800aa414 addiu  $s0, 0x0001
800aa418 andi   $v0, $s0, 0x00ff
800aa41c sltiu  $v0, 0x0003
800aa420 bnez   $v0, 0x800aa3d0
800aa424 nop    
800aa3d0 beqz   $s3, 0x800aa3f4
800aa3d4 nop    
800aa3d8 jal    0x800aa5f4
800aa3dc andi   $a0, $s0, 0x00ff
800aa5f4 addiu  $sp, -0x0020
800aa5f8 sw     $s0, 0x0010(sp)
800aa5fc andi   $s0, $a0, 0x00ff
800aa600 move   $a0, $s0
800aa604 sw     $ra, 0x0018(sp)
800aa608 jal    0x801db524
800aa60c sw     $s1, 0x0014(sp)
801db524 andi   $v1, $a0, 0x00ff
801db528 sltiu  $v0, $v1, 0x0003
801db52c beqz   $v0, 0x801db56c
801db530 sll    $v0, $v1, 0x02
801db534 addu   $v0, $v1
801db538 sll    $v1, $v0, 0x06
801db53c lui    $at, 0x8014
801db540 addu   $at, $v1
801db544 lbu    $v0, 0x5e90(at)
801db548 nop    
801db54c andi   $v0, 0x0001
801db550 beqz   $v0, 0x801db5c4
801db554 li     $v0, 0x0001
801db558 lui    $at, 0x8014
801db55c addu   $at, $v1
801db560 lhu    $v0, 0x5f10(at)
801db564 j      0x801db5b8
801db568 andi   $v0, 0x4000
801db5b8 bnez   $v0, 0x801db5c4
801db5bc li     $v0, 0x0001
801db5c0 move   $v0, $r0
801db5c4 jr     $ra
801db5c8 nop    
800aa610 andi   $v0, 0x00ff
800aa614 bnez   $v0, 0x800aa788
800aa618 move   $v0, $r0
800aa61c sll    $v0, $s0, 0x02
800aa620 addu   $v0, $s0
800aa624 sll    $s1, $v0, 0x06
800aa628 lui    $at, 0x8014
800aa62c addu   $at, $s1
800aa630 lw     $v0, 0x5fb4(at)
800aa634 nop    
800aa638 andi   $v0, 0x0001
800aa63c beqz   $v0, 0x800aa788
800aa640 move   $v0, $r0
800aa644 lui    $at, 0x8014
800aa648 addu   $at, $s1
800aa64c lbu    $v1, 0x5fa8(at)
800aa650 lui    $v0, 0x8014
800aa654 lbu    $v0, 0x6374(v0)
800aa658 nop    
800aa65c bne    $v1, $v0, 0x800aa788
800aa660 move   $v0, $r0
800aa664 lui    $v0, 0x8014
800aa668 lw     $v0, 0x6380(v0)
800aa66c nop    
800aa670 lbu    $a0, 0x0002(v0)
800aa674 jal    0x800aa874
800aa678 nop    
800aa874 andi   $a0, 0x00ff
800aa878 srl    $v0, $a0, 0x05
800aa87c sll    $v0, 0x02
800aa880 andi   $a0, 0x001f
800aa884 li     $v1, 0x0001
800aa888 lui    $at, 0x8014
800aa88c addu   $at, $v0
800aa890 lw     $v0, 0x4f80(at)
800aa894 sllv   $v1, $a0
800aa898 and    $v0, $v1
800aa89c jr     $ra
800aa8a0 sltu   $v0, $r0, $v0
800aa67c andi   $v0, 0x00ff
800aa680 bnez   $v0, 0x800aa788
800aa684 move   $v0, $r0
800aa688 jal    0x800aa8a4
800aa68c move   $a0, $s0
800aa8a4 move   $a1, $r0
800aa8a8 andi   $a0, 0x00ff
800aa8ac sll    $v0, $a0, 0x02
800aa8b0 addu   $v0, $a0
800aa8b4 sll    $v0, 0x06
800aa8b8 lui    $v1, 0x8014
800aa8bc addiu  $v1, 0x5f7e
800aa8c0 addu   $v1, $v0, $v1
800aa8c4 andi   $v0, $a1, 0x00ff
800aa8c8 addu   $v0, $v1, $v0
800aa8cc lbu    $v0, 0x0000(v0)
800aa8d0 nop    
800aa8d4 beqz   $v0, 0x800aa8f4
800aa8d8 move   $v0, $r0
800aa8dc addiu  $a1, 0x0001
800aa8e0 andi   $v0, $a1, 0x00ff
800aa8e4 sltiu  $v0, 0x000a
800aa8e8 bnez   $v0, 0x800aa8c8
800aa8ec andi   $v0, $a1, 0x00ff
800aa8c8 addu   $v0, $v1, $v0
800aa8cc lbu    $v0, 0x0000(v0)
800aa8d0 nop    
800aa8d4 beqz   $v0, 0x800aa8f4
800aa8d8 move   $v0, $r0
800aa8dc addiu  $a1, 0x0001
800aa8e0 andi   $v0, $a1, 0x00ff
800aa8e4 sltiu  $v0, 0x000a
800aa8e8 bnez   $v0, 0x800aa8c8
800aa8ec andi   $v0, $a1, 0x00ff
800aa8c8 addu   $v0, $v1, $v0
800aa8cc lbu    $v0, 0x0000(v0)
800aa8d0 nop    
800aa8d4 beqz   $v0, 0x800aa8f4
800aa8d8 move   $v0, $r0
800aa8dc addiu  $a1, 0x0001
800aa8e0 andi   $v0, $a1, 0x00ff
800aa8e4 sltiu  $v0, 0x000a
800aa8e8 bnez   $v0, 0x800aa8c8
800aa8ec andi   $v0, $a1, 0x00ff
800aa8c8 addu   $v0, $v1, $v0
800aa8cc lbu    $v0, 0x0000(v0)
800aa8d0 nop    
800aa8d4 beqz   $v0, 0x800aa8f4
800aa8d8 move   $v0, $r0
800aa8dc addiu  $a1, 0x0001
800aa8e0 andi   $v0, $a1, 0x00ff
800aa8e4 sltiu  $v0, 0x000a
800aa8e8 bnez   $v0, 0x800aa8c8
800aa8ec andi   $v0, $a1, 0x00ff
800aa8c8 addu   $v0, $v1, $v0
800aa8cc lbu    $v0, 0x0000(v0)
800aa8d0 nop    
800aa8d4 beqz   $v0, 0x800aa8f4
800aa8d8 move   $v0, $r0
800aa8f4 jr     $ra
800aa8f8 nop    
800aa690 andi   $v0, 0x00ff
800aa694 bnez   $v0, 0x800aa788
800aa698 move   $v0, $r0
800aa69c lui    $at, 0x8014
800aa6a0 addu   $at, $s1
800aa6a4 lbu    $v0, 0x5f09(at)
800aa6a8 lui    $at, 0x8018
800aa6ac addu   $at, $v0
800aa6b0 lbu    $v1, 0x1b10(at)
800aa6b4 li     $v0, 0x0006
800aa6b8 beq    $v1, $v0, 0x800aa708
800aa6bc nop    
800aa6c0 lui    $v0, 0x8014
800aa6c4 lw     $v0, 0x6380(v0)
800aa6c8 nop    
800aa6cc lhu    $v1, 0x0002(v0)
800aa6d0 nop    
800aa6d4 sll    $v0, $v1, 0x02
800aa6d8 addu   $v0, $v1
800aa6dc sll    $v0, 0x02
800aa6e0 lui    $at, 0x801d
800aa6e4 addu   $at, $v0
800aa6e8 lbu    $v0, -0x58e7(at)
800aa6ec nop    
800aa6f0 srl    $v0, 0x04
800aa6f4 lui    $at, 0x800b
800aa6f8 addu   $at, $v0
800aa6fc lbu    $s0, 0x50dc(at)
800aa700 j      0x800aa748
800aa704 nop    
800aa748 jal    0x8017e3d4
800aa74c nop    
8017e3d4 li     $t2, 0x00a0
8017e3d8 jr     $t2
8017e3dc li     $t1, 0x002f
000000a0 lui    $t0, 0x0000
000000a4 addiu  $t0, 0x05c4
000000a8 jr     $t0
000000ac nop    
000005c4 li     $t0, 0x0200
000005c8 sll    $t1, 0x02
000005cc add    $t0, $t1
000005d0 lw     $t0, 0x0000(t0)
000005d4 nop    
000005d8 jr     $t0
000005dc nop    
bfc02200 lui    $v1, 0xa001
bfc02204 lw     $v1, -0x6ff0(v1)
bfc02208 lui    $at, 0x41c6
bfc0220c ori    $at, 0x4e6d
bfc02210 multu  $v1, $at
bfc02214 lui    $at, 0xa001
bfc02218 mflo   $v1, $lo
bfc0221c addiu  $v1, 0x3039
bfc02220 srl    $v0, $v1, 0x10
bfc02224 andi   $v0, 0x7fff
bfc02228 jr     $ra
bfc0222c sw     $v1, -0x6ff0(at)
800aa750 div    $v0, $s0
800aa754 bnez   $s0, 0x800aa760
800aa758 nop    
800aa760 li     $at, -0x0001
800aa764 bne    $s0, $at, 0x800aa778
800aa768 lui    $at, 0x8000
800aa778 mfhi   $v0, $hi
800aa77c nop    
800aa780 andi   $v0, 0x00ff
800aa784 sltiu  $v0, 0x0001
800aa788 lw     $ra, 0x0018(sp)
800aa78c lw     $s1, 0x0014(sp)
800aa790 lw     $s0, 0x0010(sp)
800aa794 addiu  $sp, 0x0020
800aa798 jr     $ra
800aa79c nop    
800aa3e0 andi   $v0, 0x00ff
800aa3e4 bnez   $v0, 0x800aa408
800aa3e8 andi   $v0, $s1, 0x00ff
800aa3ec j      0x800aa418
800aa3f0 addiu  $s0, 0x0001
800aa418 andi   $v0, $s0, 0x00ff
800aa41c sltiu  $v0, 0x0003
800aa420 bnez   $v0, 0x800aa3d0
800aa424 nop    
800aa428 j      0x800aa548
800aa42c andi   $s0, $s1, 0x00ff
800aa548 beqz   $s0, 0x800aa5d0
800aa54c nop    
800aa550 jal    0x8017e3d4
800aa554 nop    
8017e3d4 li     $t2, 0x00a0
8017e3d8 jr     $t2
8017e3dc li     $t1, 0x002f
000000a0 lui    $t0, 0x0000
000000a4 addiu  $t0, 0x05c4
000000a8 jr     $t0
000000ac nop    
000005c4 li     $t0, 0x0200
000005c8 sll    $t1, 0x02
000005cc add    $t0, $t1
000005d0 lw     $t0, 0x0000(t0)
000005d4 nop    
000005d8 jr     $t0
000005dc nop    
bfc02200 lui    $v1, 0xa001
bfc02204 lw     $v1, -0x6ff0(v1)
bfc02208 lui    $at, 0x41c6
bfc0220c ori    $at, 0x4e6d
bfc02210 multu  $v1, $at
bfc02214 lui    $at, 0xa001
bfc02218 mflo   $v1, $lo
bfc0221c addiu  $v1, 0x3039
bfc02220 srl    $v0, $v1, 0x10
bfc02224 andi   $v0, 0x7fff
bfc02228 jr     $ra
bfc0222c sw     $v1, -0x6ff0(at)
800aa558 div    $v0, $s0
800aa55c bnez   $s0, 0x800aa568
800aa560 nop    
800aa568 li     $at, -0x0001
800aa56c bne    $s0, $at, 0x800aa580
800aa570 lui    $at, 0x8000
800aa580 mfhi   $v1, $hi
800aa584 nop    
800aa588 addu   $v0, $sp, $v1
800aa58c lbu    $a0, 0x0010(v0)
800aa590 li     $a1, 0x000a
800aa594 sll    $v1, $a0, 0x02
800aa598 addu   $v1, $a0
800aa59c sll    $v1, 0x06
800aa5a0 lui    $at, 0x8014
800aa5a4 addu   $at, $v1
800aa5a8 lw     $a0, 0x5fb4(at)
800aa5ac lui    $at, 0x8014
800aa5b0 addu   $at, $v1
800aa5b4 sb     $a1, 0x5e91(at)
800aa5b8 ori    $a0, 0x0008 ; activate the learning bit
800aa5bc lui    $at, 0x8014
800aa5c0 addu   $at, $v1
800aa5c4 sw     $a0, 0x5fb4(at) ; store the learning status for the current character
```