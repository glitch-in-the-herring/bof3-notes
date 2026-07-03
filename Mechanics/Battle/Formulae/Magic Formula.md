The magic formula is:

$$
d = \begin{cases}
\frac{1}{2}\delta & \text{target has barrier}\\
\delta & \text{otherwise}
\end{cases}
$$
$$
INT_A' = INT_A + \left\lfloor\frac{ INT_A\cdot \mathcal{M}}{2}\right\rfloor
$$
$$
\alpha = \left\lfloor\frac{100P(100 + INT_A')}{100}\right\rfloor
$$
$$
\beta = \begin{cases}
100 - \left\lfloor\frac{INT_D}{5}\right\rfloor & 100 - \left\lfloor\frac{INT_D}{5}\right\rfloor \geq 50 \\
50 & 100 - \left\lfloor\frac{INT_D}{5}\right\rfloor < 50
\end{cases}
$$
$$
\gamma = \left\lfloor\frac{\sum R_i\left\lfloor\frac{\alpha\beta}{100}\right\rfloor}{100}\right\rfloor
$$
$$
\delta = \left\lfloor\frac{M\gamma}{10000}\right\rfloor
$$
Where:
* $\mathcal{M}$ is the meditation counter of the attacker
* $P$ is the spell's power
* $M$ is a random multiplier from one of:
	* 85, 90, 95, 100, 105, 110, 115, 120
	* See [[Multipliers#Magic Formula|Multipliers]] for the location of these multipliers
* $R_i$ is the $i$-th resistance multiplier. This is summed up as $\sum R_i$, the total resistance multiplier. 
```
8009dcfc lbu    $a2, -0x58e5(at) ; spell pwr
8009dd00 jal    0x800a2880
8009dd04 move   $a3, $r0
800a2880 lui    $v1, 0x801f
800a2884 lhu    $v1, -0x3cee(v1) ; attacker's INT
800a2888 andi   $a2, 0xffff
800a288c addiu  $v1, 0x0064 ; attacker's INT + 100
800a2890 sll    $v0, $v1, 0x01 ; 2(attacker's INT + 100) 
800a2894 addu   $v0, $v1 ; 3(attacker's INT + 100) 
800a2898 sll    $v0, 0x03 ; 24(attacker's INT + 100) 
800a289c addu   $v0, $v1 ; 25(attacker's INT + 100) 
800a28a0 sll    $v0, 0x02 ; 100(attacker's INT + 100) 
800a28a4 mult   $a2, $v0 ; spell pwr * 100(attacker's INT + 100)
800a28a8 mflo   $a0, $lo
800a28ac lui    $v1, 0x801f
800a28b0 lhu    $v1, -0x3d0e(v1) ; defender's INT
800a28b4 lui    $v0, 0xcccc
800a28b8 ori    $v0, 0xcccd
800a28bc multu  $v1, $v0  
800a28c0 mfhi   $v0, $hi
800a28c4 lui    $a2, 0x51eb
800a28c8 ori    $a2, 0x851f
800a28cc multu  $a0, $a2 
800a28d0 addiu  $sp, -0x0020
800a28d4 sw     $s1, 0x0014(sp)
800a28d8 move   $s1, $a1
800a28dc sw     $ra, 0x0018(sp)
800a28e0 sw     $s0, 0x0010(sp)
800a28e4 srl    $v1, $v0, 0x02 ; defender's INT / 5
800a28e8 li     $v0, 0x0064
800a28ec subu   $v1, $v0, $v1 ; 100 - defender's INT / 5, let this be beta
800a28f0 slti   $v0, $v1, 0x0032 ; if 100 - defender's INT / 5 is less than 50, set beta to 50
800a28f4 mfhi   $t1, $hi 
800a28f8 beqz   $v0, 0x800a2904
800a28fc srl    $s0, $t1, 0x05 ; spell pwr * 100(attacker's INT + 100) / 100, let this be alpha
800a2904 mult   $s0, $v1  
800a2908 mflo   $v0, $lo ; alpha * beta
800a290c nop    
800a2910 nop    
800a2914 multu  $v0, $a2 
800a2918 lui    $v1, 0x8014
800a291c lhu    $v1, 0x63c0(v1)
800a2920 nop    
800a2924 sll    $v0, $v1, 0x02
800a2928 addu   $v0, $v1
800a292c sll    $v0, 0x02
800a2930 lui    $at, 0x801d
800a2934 addu   $at, $v0
800a2938 lhu    $v0, -0x58e4(at) ; load spell's element
800a293c nop    
800a2940 andi   $a1, $v0, 0x01ff
800a2944 mfhi   $t0, $hi 
800a2948 beqz   $a1, 0x800a29a0
800a294c srl    $s0, $t0, 0x05 ; alpha * beta / 100

; if the spell is elemental
800a2950 andi   $v0, $a3, 0x00ff
800a2954 beqz   $v0, 0x800a296c
800a2958 nop    
800a296c jal    0x800a2ae0
800a2970 andi   $a0, $s1, 0x00ff
800a2ae0 andi   $a0, 0x00ff
800a2ae4 sltiu  $v0, $a0, 0x0003
800a2ae8 beqz   $v0, 0x800a2c04
800a2aec move   $a2, $r0
800a2c04 andi   $v0, $a1, 0x0001 
800a2c08 beqz   $v0, 0x800a2c44

; if the spell has a fire element
800a2c0c addiu  $v0, $a0, -0x0003
800a2c10 sll    $v1, $v0, 0x03
800a2c14 addu   $v1, $v0
800a2c18 sll    $v1, 0x02
800a2c1c subu   $v1, $v0
800a2c20 sll    $v1, 0x03
800a2c24 lui    $at, 0x801f
800a2c28 addu   $at, $v1
800a2c2c lbu    $v0, -0x4921(at) ; load fire resistance 
800a2c30 nop    
800a2c34 sll    $v0, 0x01
800a2c38 lui    $at, 0x800b
800a2c3c addu   $at, $v0
800a2c40 lh     $a2, 0x493c(at) ; load fire resistance multiplier
800a2c44 andi   $v0, $a1, 0x0002
800a2c48 beqz   $v0, 0x800a2c8c

; if the spell has an ice element
800a2c4c addiu  $v1, $a0, -0x0003
800a2c50 sll    $v0, $v1, 0x03
800a2c54 addu   $v0, $v1
800a2c58 sll    $v0, 0x02
800a2c5c subu   $v0, $v1
800a2c60 sll    $v0, 0x03
800a2c64 lui    $at, 0x801f
800a2c68 addu   $at, $v0
800a2c6c lbu    $v0, -0x4920(at) ; load ice resistance
800a2c70 nop    
800a2c74 sll    $v0, 0x01
800a2c78 lui    $at, 0x800b
800a2c7c addu   $at, $v0
800a2c80 lh     $v0, 0x493c(at) ; load ice resistance multiplier
800a2c84 nop    
800a2c88 addu   $a2, $v0 ; add ice resistance multiplier to total multiplier
800a2c8c andi   $v0, $a1, 0x0004
800a2c90 beqz   $v0, 0x800a2cd4

; if the spell has a thunder element
800a2c94 addiu  $v1, $a0, -0x0003
800a2c98 sll    $v0, $v1, 0x03
800a2c9c addu   $v0, $v1
800a2ca0 sll    $v0, 0x02
800a2ca4 subu   $v0, $v1
800a2ca8 sll    $v0, 0x03
800a2cac lui    $at, 0x801f
800a2cb0 addu   $at, $v0
800a2cb4 lbu    $v0, -0x491f(at) ; load thunder resistance
800a2cb8 nop    
800a2cbc sll    $v0, 0x01
800a2cc0 lui    $at, 0x800b
800a2cc4 addu   $at, $v0
800a2cc8 lh     $v0, 0x493c(at) ; load thunder resistance multiplier
800a2ccc nop    
800a2cd0 addu   $a2, $v0 ; add thunder resistance multiplier to total multiplier 
800a2cd4 andi   $v0, $a1, 0x0008
800a2cd8 beqz   $v0, 0x800a2d1c

; if spell has earth resistance
800a2cdc addiu  $v1, $a0, -0x0003
800a2ce0 sll    $v0, $v1, 0x03
800a2ce4 addu   $v0, $v1
800a2ce8 sll    $v0, 0x02
800a2cec subu   $v0, $v1
800a2cf0 sll    $v0, 0x03
800a2cf4 lui    $at, 0x801f
800a2cf8 addu   $at, $v0
800a2cfc lbu    $v0, -0x491e(at) ; load earth resistance
800a2d00 nop    
800a2d04 sll    $v0, 0x01
800a2d08 lui    $at, 0x800b
800a2d0c addu   $at, $v0
800a2d10 lh     $v0, 0x493c(at) ; load earth resistance multiplier
800a2d14 nop    
800a2d18 addu   $a2, $v0 ; add earth resistance multiplier to total multiplier
800a2d1c andi   $v0, $a1, 0x0010 ; if the spell has wind element
800a2d20 beqz   $v0, 0x800a2d64
800a2d24 addiu  $v1, $a0, -0x0003
800a2d28 sll    $v0, $v1, 0x03
800a2d2c addu   $v0, $v1
800a2d30 sll    $v0, 0x02
800a2d34 subu   $v0, $v1
800a2d38 sll    $v0, 0x03
800a2d3c lui    $at, 0x801f
800a2d40 addu   $at, $v0
800a2d44 lbu    $v0, -0x491d(at) ; load wind resistance
800a2d48 nop    
800a2d4c sll    $v0, 0x01
800a2d50 lui    $at, 0x800b
800a2d54 addu   $at, $v0
800a2d58 lh     $v0, 0x493c(at) ; load wind resistance multiplier
800a2d5c nop    
800a2d60 addu   $a2, $v0 ; add wind resistance multiplier to total multiplier
800a2d64 sll    $v0, $a2, 0x10
800a2d68 jr     $ra
800a2d6c sra    $v0, 0x10
800a2974 sll    $v0, 0x10
800a2978 sra    $v0, 0x10

800a297c mult   $s0, $v0 ; alpha * beta / 100 * R
800a2980 mflo   $v0, $lo
800a2984 lui    $v1, 0x51eb
800a2988 ori    $v1, 0x851f
800a298c mult   $v0, $v1 
800a2990 sra    $v0, 0x1f
800a2994 mfhi   $t0, $hi
800a2998 sra    $v1, $t0, 0x05 ; alpha * beta / 100 * R / 100, let this be gamma
800a299c subu   $s0, $v1, $v0
800a29a0 jal    0x8017e3d4
800a29a4 nop    
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
800a29a8 andi   $v0, 0x0007
800a29ac sll    $v0, 0x01
800a29b0 lui    $at, 0x800b
800a29b4 addu   $at, $v0
800a29b8 lhu    $v1, 0x492c(at) ; random multiplier M
800a29bc nop    
800a29c0 mult   $s0, $v1 ; gamma * m2
800a29c4 mflo   $v1, $lo
800a29c8 lui    $v0, 0x68db
800a29cc ori    $v0, 0x8bad
800a29d0 mult   $v1, $v0 
800a29d4 lui    $v0, 0x8014
800a29d8 lbu    $v0, 0x6394(v0)
800a29dc sra    $v1, 0x1f
800a29e0 sltiu  $v0, 0x0003
800a29e4 mfhi   $t0, $hi
800a29e8 sra    $a0, $t0, 0x0c ; gamma * m / 10000
800a29ec beqz   $v0, 0x800a2a14
800a29f0 subu   $s0, $a0, $v1
800a2a14 andi   $a0, $s1, 0x00ff
800a2a18 sltiu  $v0, $a0, 0x0003
800a2a1c beqz   $v0, 0x800a2a64
800a2a20 sll    $v0, $a0, 0x02
800a2a64 addiu  $v0, $a0, -0x0003
800a2a68 sll    $v1, $v0, 0x03
800a2a6c addu   $v1, $v0
800a2a70 sll    $v1, 0x02
800a2a74 subu   $v1, $v0
800a2a78 sll    $v1, 0x03
800a2a7c lui    $at, 0x801f
800a2a80 addu   $at, $v1
800a2a84 lw     $v0, -0x48cc(at)
800a2a88 nop    
800a2a8c andi   $v0, 0x0200
800a2a90 beqz   $v0, 0x800a2aa0
800a2a94 srl    $v0, $s0, 0x1f
800a2aa0 lui    $at, 0x801f
800a2aa4 addu   $at, $v1
800a2aa8 lw     $v0, -0x48d0(at)
800a2aac lui    $v1, 0x0001
800a2ab0 and    $v0, $v1
800a2ab4 beqz   $v0, 0x800a2ac4
800a2ab8 sll    $v0, $s0, 0x10
800a2ac4 sra    $v0, 0x10
800a2ac8 lw     $ra, 0x0018(sp)
800a2acc lw     $s1, 0x0014(sp)
800a2ad0 lw     $s0, 0x0010(sp)
800a2ad4 addiu  $sp, 0x0020
800a2ad8 jr     $ra
800a2adc nop    
8009dd08 lui    $v1, 0x8014
8009dd0c lw     $v1, 0x63a0(v1)
8009dd10 lw     $ra, 0x0010(sp)
8009dd14 sh     $v0, 0x0004(v1) ; store final damage
```
This code can be found at:
```
BIN/BATTLE/BATTLE.EMI: 000914fc
BIN/BATTLE/BATTLE2.EMI: 000914fc
BIN/BOSS/BOSS001.EMI: 0004ecfc
BIN/BOSS/BOSS002.EMI: 000924fc
BIN/BOSS/BOSS004.EMI: 0004ecfc
BIN/BOSS/BOSS007.EMI: 000914fc
BIN/BOSS/BOSS008.EMI: 0008f4fc
BIN/BOSS/BOSS012.EMI: 000924fc
BIN/BOSS/BOSS013.EMI: 000924fc
BIN/BOSS/BOSS014.EMI: 000914fc
BIN/BOSS/BOSS015.EMI: 000914fc
BIN/BOSS/BOSS017.EMI: 000924fc
BIN/BOSS/BOSS018.EMI: 000924fc
BIN/BOSS/BOSS019.EMI: 000924fc
BIN/BOSS/BOSS020.EMI: 000924fc
BIN/BOSS/BOSS021.EMI: 000924fc
BIN/BOSS/BOSS022.EMI: 0004ecfc
BIN/BOSS/BOSS023.EMI: 0008f4fc
BIN/BOSS/BOSS024.EMI: 000924fc
BIN/BOSS/BOSS025.EMI: 0004ecfc
BIN/BOSS/BOSS027.EMI: 000924fc
BIN/BOSS/BOSS028.EMI: 000924fc
BIN/BOSS/BOSS029.EMI: 000924fc
BIN/BOSS/BOSS030.EMI: 000924fc
BIN/BOSS/BOSS031.EMI: 0004ecfc
BIN/BOSS/BOSS032.EMI: 000924fc
BIN/BOSS/BOSS033.EMI: 000914fc
BIN/BOSS/BOSS034.EMI: 000924fc
BIN/BOSS/BOSS035.EMI: 000924fc
BIN/BOSS/BOSS036.EMI: 000924fc
BIN/BOSS/BOSS037.EMI: 000924fc
BIN/BOSS/BOSS038.EMI: 000924fc
BIN/BOSS/BOSS040.EMI: 000924fc
BIN/BOSS/BOSS042.EMI: 000924fc
BIN/BOSS/BOSS046.EMI: 000924fc
BIN/BOSS/BOSS047.EMI: 000924fc
BIN/BOSS/BOSS049.EMI: 000924fc
BIN/BOSS/BOSS050.EMI: 000924fc
BIN/BOSS/BOSS051.EMI: 000924fc
BIN/BOSS/BOSS052.EMI: 0008fcfc
BIN/BOSS/BOSS054.EMI: 000924fc
BIN/BOSS/BOSS055.EMI: 000954fc
```