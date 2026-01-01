The base damage formula for breath attacks is:
$$
d = \left\lfloor\frac{\alpha}{10000}\right\rfloor
$$
$$
\alpha = \left(\sum R_i\right)M\left\lfloor\frac{ HP_A}{\rho}\right\rfloor
$$
Where:
* $M$ is a random multiplier from one of:
	* 85, 90, 95, 100, 105, 110, 115, 120
	* See [[Multipliers#Breath Formula|Multipliers]] for the location of these multipliers
* $R_i$ is the $i$-th resistance multiplier. This is summed up as $\sum R_i$, the total resistance multiplier. For spells with elements ≥ holy, or if the spell has no elements, then this total set to 100
* $\rho$ is the "rank" of the breath spell, which are given as such:

| Rank ($\rho$) | Spells                                                                                                                                            | Spell Call | Modifications |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ------------- |
| 1             | KaiserBreath                                                                                                                                      | `0x41`     |               |
| 2             | DoomBreath<br>Aura Breath<br>Magma Breath<br>Gaea'sBreath<br>Hurricane                                                                            | `0x42`     |               |
| 2             | DragonBreath                                                                                                                                      | `0x7c`     | $d'=d-DEF_D$  |
| 3             | Firebreath<br>Icebreath<br>Flame Breath<br>Frost Breath<br>ThundrBreath<br>DivineBreath<br>[[Noting#Noting 6\|Noting 6]]<br>Geo Breath<br>Tempest | `0x40`     |               |
| 3             | Whelp Breath                                                                                                                                      | `0x06`     | $d'=d-DEF_D$  |

The ranks are determined by the [[spell call]].
The code for the breath formula can be found at:
* `0x800a4294` in the RAM
* In the following locations in the game's files:
```
BIN/BATTLE/BATTLE.EMI: 00097a94
BIN/BATTLE/BATTLE2.EMI: 00097a94
BIN/BOSS/BOSS001.EMI: 00055294
BIN/BOSS/BOSS002.EMI: 00098a94
BIN/BOSS/BOSS004.EMI: 00055294
BIN/BOSS/BOSS007.EMI: 00097a94
BIN/BOSS/BOSS008.EMI: 00095a94
BIN/BOSS/BOSS012.EMI: 00098a94
BIN/BOSS/BOSS013.EMI: 00098a94
BIN/BOSS/BOSS014.EMI: 00097a94
BIN/BOSS/BOSS015.EMI: 00097a94
BIN/BOSS/BOSS017.EMI: 00098a94
BIN/BOSS/BOSS018.EMI: 00098a94
BIN/BOSS/BOSS019.EMI: 00098a94
BIN/BOSS/BOSS020.EMI: 00098a94
BIN/BOSS/BOSS021.EMI: 00098a94
BIN/BOSS/BOSS022.EMI: 00055294
BIN/BOSS/BOSS023.EMI: 00095a94
BIN/BOSS/BOSS024.EMI: 00098a94
BIN/BOSS/BOSS025.EMI: 00055294
BIN/BOSS/BOSS027.EMI: 00098a94
BIN/BOSS/BOSS028.EMI: 00098a94
BIN/BOSS/BOSS029.EMI: 00098a94
BIN/BOSS/BOSS030.EMI: 00098a94
BIN/BOSS/BOSS031.EMI: 00055294
BIN/BOSS/BOSS032.EMI: 00098a94
BIN/BOSS/BOSS033.EMI: 00097a94
BIN/BOSS/BOSS034.EMI: 00098a94
BIN/BOSS/BOSS035.EMI: 00098a94
BIN/BOSS/BOSS036.EMI: 00098a94
BIN/BOSS/BOSS037.EMI: 00098a94
BIN/BOSS/BOSS038.EMI: 00098a94
BIN/BOSS/BOSS040.EMI: 00098a94
BIN/BOSS/BOSS042.EMI: 00098a94
BIN/BOSS/BOSS046.EMI: 00098a94
BIN/BOSS/BOSS047.EMI: 00098a94
BIN/BOSS/BOSS049.EMI: 00098a94
BIN/BOSS/BOSS050.EMI: 00098a94
BIN/BOSS/BOSS051.EMI: 00098a94
BIN/BOSS/BOSS052.EMI: 00096294
BIN/BOSS/BOSS054.EMI: 00098a94
BIN/BOSS/BOSS055.EMI: 0009ba94
```

```
800a4294 lui    $v1, 0x8014
800a4298 lbu    $v1, 0x6374(v1)
800a429c addiu  $sp, -0x0020
800a42a0 sw     $s2, 0x0018(sp)
800a42a4 move   $s2, $a0
800a42a8 sw     $ra, 0x001c(sp)
800a42ac sw     $s1, 0x0014(sp)
800a42b0 sltiu  $v0, $v1, 0x0003
800a42b4 beqz   $v0, 0x800a42dc
800a42b8 sw     $s0, 0x0010(sp)
800a42bc sll    $v0, $v1, 0x02
800a42c0 addu   $v0, $v1
800a42c4 sll    $v0, 0x06
800a42c8 lui    $at, 0x8014
800a42cc addu   $at, $v0
800a42d0 lhu    $s0, 0x5f18(at) ; attacker's HP
800a42d4 j      0x800a4300
800a42d8 nop    
800a4300 lui    $v0, 0x8014
800a4304 lhu    $v0, 0x63c0(v0) ; load spell ID
800a4308 nop    
800a430c sll    $v1, $v0, 0x02
800a4310 addu   $v1, $v0
800a4314 sll    $v1, 0x02
800a4318 lui    $at, 0x801d
800a431c addu   $at, $v1
800a4320 lhu    $v0, -0x58e4(at) ; load spell's element
800a4324 nop    
800a4328 andi   $a1, $v0, 0x01ff 
800a432c andi   $v0, 0x001f ; get the magic elements
800a4330 beqz   $v0, 0x800a4350

; if the spell has no magic element
800a4334 li     $s1, 0x0064 ; set the resistance multiplier R to 0

; if the spell has a magic element
800a4338 lui    $a0, 0x8014
800a433c lbu    $a0, 0x6394(a0) ; load target's ID
800a4340 jal    0x800a2ae0
800a4344 nop    
800a2ae0 andi   $a0, 0x00ff
800a2ae4 sltiu  $v0, $a0, 0x0003
800a2ae8 beqz   $v0, 0x800a2c04
800a2aec move   $a2, $r0 ; set the total resistance multiplier to 0
800a2c04 andi   $v0, $a1, 0x0001 ; check the element for fire
800a2c08 beqz   $v0, 0x800a2c44
800a2c0c addiu  $v0, $a0, -0x0003

; if there is fire
800a2c10 sll     $v1, $v0, 0x03
800a2c14 addu    $v1, $v0
800a2c18 sll     $v1, 0x02
800a2c1c subu    $v1, $v0
800a2c20 sll     $v1, 0x03
800a2c24 lui     $at, 0x801f
800a2c28 addu    $at, $v1
800a2c2c lbu     $v0, -0x4921(at) ; load the target's fire resistance
800a2c30 nop
800a2c34 sll     $v0, 0x01
800a2c38 lui     $at, 0x800b
800a2c3c addu    $at, $v0
800a2c40 lh      $a2, 0x493c(at) ; load the fire resistance multiplier

800a2c44 andi   $v0, $a1, 0x0002 ; check the element for ice
800a2c48 beqz   $v0, 0x800a2c8c
800a2c4c addiu  $v1, $a0, -0x0003

; if there is ice
800a2c50 sll    $v0, $v1, 0x03
800a2c54 addu   $v0, $v1
800a2c58 sll    $v0, 0x02
800a2c5c subu   $v0, $v1
800a2c60 sll    $v0, 0x03
800a2c64 lui    $at, 0x801f
800a2c68 addu   $at, $v0
800a2c6c lbu    $v0, -0x4920(at) ; load the target's ice resistance
800a2c70 nop    
800a2c74 sll    $v0, 0x01
800a2c78 lui    $at, 0x800b
800a2c7c addu   $at, $v0
800a2c80 lh     $v0, 0x493c(at) ; load the ice multiplier
800a2c84 nop    
800a2c88 addu   $a2, $v0 ; add the ice multiplier to the total

800a2c8c andi   $v0, $a1, 0x0004 ; check the element for thunder
800a2c90 beqz   $v0, 0x800a2cd4
800a2c94 addiu  $v1, $a0, -0x0003

; if there is thunder
800a2c98 sll    $v0, $v1, 0x03
800a2c9c addu   $v0, $v1
800a2ca0 sll    $v0, 0x02
800a2ca4 subu   $v0, $v1
800a2ca8 sll    $v0, 0x03
800a2cac lui    $at, 0x801f
800a2cb0 addu   $at, $v0
800a2cb4 lbu    $v0, -0x491f(at) ; load the target's thunder resistance
800a2cb8 nop    
800a2cbc sll    $v0, 0x01
800a2cc0 lui    $at, 0x800b
800a2cc4 addu   $at, $v0
800a2cc8 lh     $v0, 0x493c(at) ; load the thunder multiplier
800a2ccc nop    
800a2cd0 addu   $a2, $v0 ; add the thunder multiplier to the total

800a2cd4 andi   $v0, $a1, 0x0008 ; check the element for earth
800a2cd8 beqz   $v0, 0x800a2d1c
800a2cdc addiu  $v1, $a0, -0x0003

; if there is earth
800a2ce0 sll    $v0, $v1, 0x03
800a2ce4 addu   $v0, $v1
800a2ce8 sll    $v0, 0x02
800a2cec subu   $v0, $v1
800a2cf0 sll    $v0, 0x03
800a2cf4 lui    $at, 0x801f
800a2cf8 addu   $at, $v0
800a2cfc lbu    $v0, -0x491e(at) ; load the target's earth resistance
800a2d00 nop    
800a2d04 sll    $v0, 0x01
800a2d08 lui    $at, 0x800b
800a2d0c addu   $at, $v0
800a2d10 lh     $v0, 0x493c(at) ; load the earth multiplier
800a2d14 nop    
800a2d18 addu   $a2, $v0 ; add the earth multiplier to the total

800a2d1c andi   $v0, $a1, 0x0010 ; check the element for wind
800a2d20 beqz   $v0, 0x800a2d64
800a2d24 addiu  $v1, $a0, -0x0003

; if there is wind
800a2d28 sll    $v0, $v1, 0x03
800a2d2c addu   $v0, $v1
800a2d30 sll    $v0, 0x02
800a2d34 subu   $v0, $v1
800a2d38 sll    $v0, 0x03
800a2d3c lui    $at, 0x801f
800a2d40 addu   $at, $v0
800a2d44 lbu    $v0, -0x491d(at) ; load the target's wind resistance
800a2d48 nop    
800a2d4c sll    $v0, 0x01
800a2d50 lui    $at, 0x800b
800a2d54 addu   $at, $v0
800a2d58 lh     $v0, 0x493c(at) ; load the wind resistance multiplier
800a2d5c nop    
800a2d60 addu   $a2, $v0 ; add the wind multiplier to the total, let this be R

800a2d64 sll    $v0, $a2, 0x10
800a2d68 jr     $ra
800a2d6c sra    $v0, 0x10
800a4348 sll    $v0, 0x10
800a434c sra    $s1, $v0, 0x10
800a4350 jal    0x8017e3d4 ; call random()
800a4354 nop    
...
800a4358 div    $s0, $s2 ; attacker's HP / rank
800a435c bnez   $s2, 0x800a4368
800a4360 nop    
800a4368 li     $at, -0x0001
800a436c bne    $s2, $at, 0x800a4380
800a4370 lui    $at, 0x8000
800a4380 mflo   $v1, $lo
800a4384 andi   $v0, 0x0007
800a4388 sll    $v0, 0x01
800a438c lui    $at, 0x800b
800a4390 addu   $at, $v0
800a4394 lh     $v0, 0x498c(at) ; load random multiplier
800a4398 nop    
800a439c mult   $v1, $v0 ; HP / rank * random multiplier
800a43a0 mflo   $v1, $lo
800a43a4 nop    
800a43a8 nop    
800a43ac mult   $v1, $s1 ; HP / rank * M * R, let this be alpha
800a43b0 mflo   $v0, $lo
800a43b4 lui    $v1, 0x68db
800a43b8 ori    $v1, 0x8bad
800a43bc mult   $v0, $v1
800a43c0 lui    $a0, 0x8014
800a43c4 lbu    $a0, 0x6394(a0)
800a43c8 sra    $v0, 0x1f
800a43cc mfhi   $a2, $hi
800a43d0 sra    $v1, $a2, 0x0c ; alpha / 10000, this is the raw breath damage
800a43d4 subu   $s1, $v1, $v0
800a43d8 sltiu  $v0, $a0, 0x0003
800a43dc beqz   $v0, 0x800a4400
800a43e0 sll    $v0, $a0, 0x02
800a4400 addiu  $v1, $a0, -0x0003
800a4404 sll    $v0, $v1, 0x03
800a4408 addu   $v0, $v1
800a440c sll    $v0, 0x02
800a4410 subu   $v0, $v1
800a4414 sll    $v0, 0x03
800a4418 lui    $at, 0x801f
800a441c addu   $at, $v0
800a4420 lw     $v0, -0x48d0(at)
800a4424 lui    $v1, 0x0001
800a4428 and    $v0, $v1
800a442c bnez   $v0, 0x800a443c
800a4430 move   $v0, $r0
800a4434 sll    $v0, $s1, 0x10
800a4438 sra    $v0, 0x10
800a443c lw     $ra, 0x001c(sp)
800a4440 lw     $s2, 0x0018(sp)
800a4444 lw     $s1, 0x0014(sp)
800a4448 lw     $s0, 0x0010(sp)
800a444c addiu  $sp, 0x0020
```