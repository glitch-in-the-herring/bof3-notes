The standard healing spells use the following formula to determine the amount of HP healed in battle:
$$
d = \left\lfloor\frac{R\beta}{10000}\right\rfloor
$$
$$
\alpha = {100(100+INT_A)}
$$
$$
\beta = \left\lfloor\frac{\alpha P}{100}\right\rfloor
$$```
```
800a30ec lhu    $a0, -0x3cee(a0) ; caster's int
800a30f0 lui    $v0, 0x8014
800a30f4 lhu    $v0, 0x63c0(v0)
800a30f8 addiu  $a0, 0x0064 ; caster's int + 100
800a30fc sll    $v1, $v0, 0x02
800a3100 addu   $v1, $v0
800a3104 sll    $v1, 0x02
800a310c addu   $v0, $a0 ; (caster's int + 100) * 3
800a3108 sll    $v0, $a0, 0x01 ; (caster's int + 100) * 6
800a3110 sll    $v0, 0x03 ; (caster's int + 100) * 24
800a3114 addu   $v0, $a0 ; (caster's int + 100) * 25
800a3118 lui    $at, 0x801d
800a311c addu   $at, $v1
800a3120 lbu    $v1, -0x58e5(at) ; spell pwr
800a3124 sll    $v0, 0x02 ; (caster's int + 100) * 100, let this be alpha
800a3128 mult   $v1, $v0 ; alpha * pwr
800a312c mflo   $v1, $lo
800a3130 lui    $v0, 0x51eb
800a3134 ori    $v0, 0x851f
800a3138 multu  $v1, $v0 ; alpha * pwr / 100, let this be beta
800a313c andi   $v1, $a1, 0x00ff
800a3140 sltiu  $v0, $v1, 0x0003
800a3144 mfhi   $a2, $hi
800a3148 beqz   $v0, 0x800a3170
800a314c srl    $a0, $a2, 0x05
800a3150 sll    $v0, $v1, 0x02
800a3154 addu   $v0, $v1
800a3158 sll    $v0, 0x06
800a315c lui    $at, 0x8014
800a3160 addu   $at, $v0
800a3164 lbu    $v0, 0x5f34(at) ; load heal res
800a3168 j      0x800a319c
800a316c sll    $v0, 0x01
800a319c lui    $at, 0x800b
800a31a0 addu   $at, $v0
800a31a4 lh     $v0, 0x497c(at) ; get multiplier R
800a31a8 nop    
800a31ac mult   $a0, $v0 ; beta * R
800a31b0 mflo   $v0, $lo
800a31b4 lui    $v1, 0x68db
800a31b8 ori    $v1, 0x8bad
800a31bc mult   $v0, $v1 ; beta * R / 10000
```
The code can be found at:
```
BIN/BATTLE/BATTLE.EMI: 000968e8
BIN/BATTLE/BATTLE2.EMI: 000968e8
BIN/BOSS/BOSS001.EMI: 000540e8
BIN/BOSS/BOSS002.EMI: 000978e8
BIN/BOSS/BOSS004.EMI: 000540e8
BIN/BOSS/BOSS007.EMI: 000968e8
BIN/BOSS/BOSS008.EMI: 000948e8
BIN/BOSS/BOSS012.EMI: 000978e8
BIN/BOSS/BOSS013.EMI: 000978e8
BIN/BOSS/BOSS014.EMI: 000968e8
BIN/BOSS/BOSS015.EMI: 000968e8
BIN/BOSS/BOSS017.EMI: 000978e8
BIN/BOSS/BOSS018.EMI: 000978e8
BIN/BOSS/BOSS019.EMI: 000978e8
BIN/BOSS/BOSS020.EMI: 000978e8
BIN/BOSS/BOSS021.EMI: 000978e8
BIN/BOSS/BOSS022.EMI: 000540e8
BIN/BOSS/BOSS023.EMI: 000948e8
BIN/BOSS/BOSS024.EMI: 000978e8
BIN/BOSS/BOSS025.EMI: 000540e8
BIN/BOSS/BOSS027.EMI: 000978e8
BIN/BOSS/BOSS028.EMI: 000978e8
BIN/BOSS/BOSS029.EMI: 000978e8
BIN/BOSS/BOSS030.EMI: 000978e8
BIN/BOSS/BOSS031.EMI: 000540e8
BIN/BOSS/BOSS032.EMI: 000978e8
BIN/BOSS/BOSS033.EMI: 000968e8
BIN/BOSS/BOSS034.EMI: 000978e8
BIN/BOSS/BOSS035.EMI: 000978e8
BIN/BOSS/BOSS036.EMI: 000978e8
BIN/BOSS/BOSS037.EMI: 000978e8
BIN/BOSS/BOSS038.EMI: 000978e8
BIN/BOSS/BOSS040.EMI: 000978e8
BIN/BOSS/BOSS042.EMI: 000978e8
BIN/BOSS/BOSS046.EMI: 000978e8
BIN/BOSS/BOSS047.EMI: 000978e8
BIN/BOSS/BOSS049.EMI: 000978e8
BIN/BOSS/BOSS050.EMI: 000978e8
BIN/BOSS/BOSS051.EMI: 000978e8
BIN/BOSS/BOSS052.EMI: 000950e8
BIN/BOSS/BOSS054.EMI: 000978e8
BIN/BOSS/BOSS055.EMI: 0009a8e8
```