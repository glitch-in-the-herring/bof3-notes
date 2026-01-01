The target of the current combatant's action is stored at
* `0x80146384` in the RAM

The enemy uses the following formula to determine the target of an action, if it selects an action that would normally target the player's party and has no active special targeting behavior:
$$
\DeclareMathOperator*{\argmin}{argmin\,}
i=\min \left[\argmin_{0\leq n\leq 2} {f\left(r, \sum_{k=0}^nw_i\right)}\right]
$$

$$
f(n, k) = \begin{cases}
1 & n \geq k\\
0 & n < k
\end{cases}
$$
$$
d = \sum_{k=0}^{2} w_k
$$
$$
r = \mathrm{random}(0,d-1)
$$
Where:
* $i$ is the index of the combatant selected. This is always from the player's party ($0\leq i\leq2$)
* $w_k$ is the weights of the positions of the current formation
In all formations, $d$ is 16.
The weights for each formation can be found at:
* `0x801eb39c` in the RAM
* In the following places in the game's files:
```
BIN/BATTLE/BATTLE.EMI: 0005d79c
BIN/BATTLE/BATTLE2.EMI: 0005d79c
BIN/BOSS/BOSS001.EMI: 0001af9c
BIN/BOSS/BOSS002.EMI: 0005e79c
BIN/BOSS/BOSS004.EMI: 0001af9c
BIN/BOSS/BOSS007.EMI: 0005d79c
BIN/BOSS/BOSS008.EMI: 0005b79c
BIN/BOSS/BOSS012.EMI: 0005e79c
BIN/BOSS/BOSS013.EMI: 0005e79c
BIN/BOSS/BOSS014.EMI: 0005d79c
BIN/BOSS/BOSS015.EMI: 0005d79c
BIN/BOSS/BOSS017.EMI: 0005e79c
BIN/BOSS/BOSS018.EMI: 0005e79c
BIN/BOSS/BOSS019.EMI: 0005e79c
BIN/BOSS/BOSS020.EMI: 0005e79c
BIN/BOSS/BOSS021.EMI: 0005e79c
BIN/BOSS/BOSS022.EMI: 0001af9c
BIN/BOSS/BOSS023.EMI: 0005b79c
BIN/BOSS/BOSS024.EMI: 0005e79c
BIN/BOSS/BOSS025.EMI: 0001af9c
BIN/BOSS/BOSS027.EMI: 0005e79c
BIN/BOSS/BOSS028.EMI: 0005e79c
BIN/BOSS/BOSS029.EMI: 0005e79c
BIN/BOSS/BOSS030.EMI: 0005e79c
BIN/BOSS/BOSS031.EMI: 0001af9c
BIN/BOSS/BOSS032.EMI: 0005e79c
BIN/BOSS/BOSS033.EMI: 0005d79c
BIN/BOSS/BOSS034.EMI: 0005e79c
BIN/BOSS/BOSS035.EMI: 0005e79c
BIN/BOSS/BOSS036.EMI: 0005e79c
BIN/BOSS/BOSS037.EMI: 0005e79c
BIN/BOSS/BOSS038.EMI: 0005e79c
BIN/BOSS/BOSS040.EMI: 0005e79c
BIN/BOSS/BOSS042.EMI: 0005e79c
BIN/BOSS/BOSS046.EMI: 0005e79c
BIN/BOSS/BOSS047.EMI: 0005e79c
BIN/BOSS/BOSS049.EMI: 0005e79c
BIN/BOSS/BOSS050.EMI: 0005e79c
BIN/BOSS/BOSS051.EMI: 0005e79c
BIN/BOSS/BOSS052.EMI: 0005bf9c
BIN/BOSS/BOSS054.EMI: 0005e79c
BIN/BOSS/BOSS055.EMI: 0006179c
```
Each weight is a byte. Each formation has three weights.
## Normal

| Position | Weight | Probability |
| -------- | ------ | ----------- |
| 0        | 6      | 37.5%       |
| 1        | 6      | 37.5%       |
| 2        | 4      | 25%         |
## Attack
| Position | Weight | Probability |
| -------- | ------ | ----------- |
| 0        | 10     | 62.5%       |
| 1        | 3      | 18.75%      |
| 2        | 3      | 18.75%      |
## Defense
| Position | Weight | Probability |
| -------- | ------ | ----------- |
| 0        | 6      | 37.5%       |
| 1        | 5      | 31.25%      |
| 2        | 5      | 31.25%      |
## Chain
| Position | Weight | Probability |
| -------- | ------ | ----------- |
| 0        | 8      | 50%         |
| 1        | 5      | 31.25%      |
| 2        | 3      | 18.75%      |
## Magic
| Position | Weight | Probability |
| -------- | ------ | ----------- |
| 0        | 6      | 37.5%       |
| 1        | 6      | 37.5%       |
| 2        | 4      | 25%         |
## Refuge
| Position | Weight | Probability |
| -------- | ------ | ----------- |
| 0        | 8      | 50%         |
| 1        | 5      | 31.25%      |
| 2        | 3      | 18.75%      |
## Code
```
801e2e38 move   $s2, $r0 ; set the max roll to 0
801e2e3c sw     $s3, 0x001c(sp)
801e2e40 move   $s3, $r0 ; set the current cumulative sum to 0
801e2e44 lui    $v1, 0x8014
801e2e48 lbu    $v1, 0x62f0(v1)
801e2e4c li     $v0, 0x0002
801e2e50 sw     $ra, 0x0024(sp)
801e2e54 sw     $s4, 0x0020(sp)
801e2e58 sw     $s1, 0x0014(sp)
801e2e5c beq    $v1, $v0, 0x801e2e84
801e2e60 sw     $s0, 0x0010(sp)
801e2e64 slti   $v0, $v1, 0x0003
801e2e68 bnez   $v0, 0x801e3094
801e2e6c move   $v0, $r0
801e2e70 li     $v0, 0x0003
801e2e74 beq    $v1, $v0, 0x801e2f8c
801e2e78 move   $v0, $r0
801e2f8c move   $s0, $r0
801e2f90 lui    $s4, 0x801f
801e2f94 addiu  $s4, -0x4c64
801e2f98 andi   $s1, $s0, 0x00ff

; Loop the following three times
    801e2f9c jal    0x801db524
    801e2fa0 move   $a0, $s1
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
    801e2fa4 andi   $v0, 0x00ff
    801e2fa8 bnez   $v0, 0x801e2fd8
    801e2fac nop    
    801e2fb0 lui    $v0, 0x8014
    801e2fb4 lbu    $v0, 0x4f58(v0) ; load current formation index
    801e2fb8 nop    
    801e2fbc sll    $v1, $v0, 0x01 ; formation index *2
    801e2fc0 addu   $v1, $v0 ; formation index * 3, this is used as the base for the formation's weights
    801e2fc4 addu   $v1, $s4 ; get the base address for the formation's weights
    801e2fc8 addu   $v1, $s1 ; add the current loop's offset
    801e2fcc lbu    $v0, 0x0000(v1) ; load current weight
    801e2fd0 nop    
    801e2fd4 addu   $s2, $v0 ; add weight to max roll
    801e2fd8 addiu  $s0, 0x0001 ; add 1 to loop counter
    801e2fdc andi   $v0, $s0, 0x00ff
    801e2fe0 sltiu  $v0, 0x0003
    801e2fe4 bnez   $v0, 0x801e2f9c ; end loop after three iterations
    801e2fe8 andi   $s1, $s0, 0x00ff

; call rand()
801e2fec jal    0x8017e3d4
801e2ff0 move   $s0, $r0 ; set the loop counter to 0
...
801e2ff4 andi   $v1, $s2, 0x00ff
801e2ff8 div    $v0, $v1 
801e2ffc bnez   $v1, 0x801e3008 ; checks to make sure that the max roll isn't zero
801e3000 nop    
801e3008 li     $at, -0x0001
801e300c bne    $v1, $at, 0x801e3020 ; checks to make sure that the max roll isn't negative 1
801e3010 lui    $at, 0x8000
801e3020 mfhi   $v1, $hi ; generate a random number between 0 and max roll - 1, let this be r
801e3024 lui    $s4, 0x801f
801e3028 addiu  $s4, -0x4c64
801e302c andi   $s2, $v1, 0x00ff

    ; Loop the following 3 times
    801e3030 andi   $s1, $s0, 0x00ff ; sets the currently checked position to the loop counter
    801e3034 jal    0x801db524
    801e3038 move   $a0, $s1
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
    801e303c andi   $v0, 0x00ff
    801e3040 bnez   $v0, 0x801e3080
    801e3044 nop    
    801e3048 lui    $v1, 0x8014
    801e304c lbu    $v1, 0x4f58(v1) ; load current formation
    801e3050 nop    
    801e3054 sll    $v0, $v1, 0x01
    801e3058 addu   $v0, $v1
    801e305c addu   $v0, $s4
    801e3060 addu   $v0, $s1
    801e3064 lbu    $v0, 0x0000(v0) ; load current weight
    801e3068 nop    
    801e306c addu   $s3, $v0 ; add to cumulative sum
    801e3070 andi   $v0, $s3, 0x00ff
    801e3074 sltu   $v0, $s2, $v0
    801e3078 bnez   $v0, 0x801e3094
    801e307c move   $v0, $s1

    ; if the current cumulative sum is less than r
    801e3080 addiu  $s0, 0x0001 ; add 1 to the loop counter
    801e3084 andi   $v1, $s0, 0x00ff
    801e3088 sltiu  $v0, $v1, 0x0003
    801e308c bnez   $v0, 0x801e3030
    801e3090 move   $v0, $v1 ; move the current position to v0

; if the current cumulative sum is greater than or equal to r: ends loop
801e3094 lw     $ra, 0x0024(sp)
801e3098 lw     $s4, 0x0020(sp)
801e309c lw     $s3, 0x001c(sp)
801e30a0 lw     $s2, 0x0018(sp)
801e30a4 lw     $s1, 0x0014(sp)
801e30a8 lw     $s0, 0x0010(sp)
801e30ac addiu  $sp, 0x0028
801e30b0 jr     $ra
801e30b4 nop    
801e2c5c j      0x801e2c94
801e2c60 andi   $v0, 0x00ff
801e2c94 lw     $ra, 0x0010(sp)
801e2c98 addiu  $sp, 0x0018
801e2c9c jr     $ra
801e2ca0 nop    
801e2868 lui    $at, 0x8014
801e286c sb     $v0, 0x6384(at) ; set the current position as the target

```