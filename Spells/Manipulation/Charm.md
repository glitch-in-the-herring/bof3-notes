
| Spell ID          | Targeting                              | Power | AP  | Element |
| ----------------- | -------------------------------------- | ----- | --- | ------- |
| `0x9e`<br>158<br> | `0x6e`<br>Single<br>Always enemy party | 0<br> | 0   | None    |

Charm increases the steal rate by 2 and the drop rate by 1. Once the rates have been increased, it sets a flag so that the spell cannot be used more than once on the same enemy.

```
800a0040 lbu    $v0, -0x4936(at) ; load current steal rate
800a0044 nop    
800a0048 beqz   $v0, 0x800a009c
800a004c andi   $v0, $a1, 0x00ff

; if it is non-zero:
800a0050 lui    $at, 0x801f
800a0054 addu   $at, $a0
800a0058 lbu    $v1, -0x4935(at) ; load current steal item charm flag
800a005c nop    
800a0060 andi   $v0, $v1, 0x0001
800a0064 bnez   $v0, 0x800a009c 
800a0068 andi   $v0, $a1, 0x00ff
 
; if it is not active:
800a006c lui    $at, 0x801f
800a0070 addu   $at, $a0
800a0074 lbu    $v0, -0x4936(at) ; load current steal rate
800a0078 ori    $v1, 0x0001 ; set the flag to active
800a007c lui    $at, 0x801f
800a0080 addu   $at, $a0
800a0084 sb     $v1, -0x4935(at) ; store flag
800a0088 addiu  $v0, 0x0002 ; add 2 to the steal rate
800a008c lui    $at, 0x801f
800a0090 addu   $at, $a0
800a0094 sb     $v0, -0x4936(at) ; store new steal rate 
800a0098 andi   $v0, $a1, 0x00ff
800a009c sll    $v1, $v0, 0x03
800a00a0 addu   $v1, $v0
800a00a4 sll    $v1, 0x02
800a00a8 subu   $v1, $v0
800a00ac sll    $a0, $v1, 0x03
800a00b0 lui    $at, 0x801f
800a00b4 addu   $at, $a0
800a00b8 lbu    $v0, -0x4932(at) ; load current drop rate
800a00bc nop    
800a00c0 beqz   $v0, 0x800a0114
800a00c4 andi   $v0, $a1, 0x00ff

; if it is not zero
800a00c8 lui    $at, 0x801f
800a00cc addu   $at, $a0
800a00d0 lbu    $v1, -0x4931(at) ; load current drop item charm flag
800a00d4 nop    
800a00d8 andi   $v0, $v1, 0x0001
800a00dc bnez   $v0, 0x800a0114
800a00e0 andi   $v0, $a1, 0x00ff

; if it is not active
800a00e4 lui    $at, 0x801f
800a00e8 addu   $at, $a0
800a00ec lbu    $v0, -0x4932(at) ; load current drop rate
800a00f0 ori    $v1, 0x0001 ; set the flag to active
800a00f4 lui    $at, 0x801f
800a00f8 addu   $at, $a0
800a00fc sb     $v1, -0x4931(at) ; store flag
800a0100 addiu  $v0, 0x0001 ; add 1 to the drop rate
800a0104 lui    $at, 0x801f
800a0108 addu   $at, $a0
800a010c sb     $v0, -0x4932(at) ; store new drop rate
800a0110 andi   $v0, $a1, 0x00ff
800a0114 sll    $v1, $v0, 0x03
800a0118 addu   $v1, $v0
800a011c sll    $v1, 0x02
800a0120 subu   $v1, $v0
800a0124 sll    $v1, 0x03
800a0128 lui    $at, 0x801f
800a012c addu   $at, $v1
800a0130 lbu    $v0, -0x4936(at) ; load new steal rate
800a0134 nop    
800a0138 sltiu  $v0, 0x0008 
800a013c bnez   $v0, 0x800a0150
800a0140 li     $v0, 0x0007

; if it is greater than or equal to 8
800a0144 lui    $at, 0x801f
800a0148 addu   $at, $v1
800a014c sb     $v0, -0x4936(at) ; cap it to 8

; if it is less than 8
800a0150 lui    $at, 0x801f
800a0154 addu   $at, $v1
800a0158 lbu    $v0, -0x4932(at) ; load new drop rate
800a015c nop    
800a0160 sltiu  $v0, 0x0008
800a0164 bnez   $v0, 0x800a0178
800a0168 li     $v0, 0x0007

; if it is greater than or equal to 8
800a016c lui    $at, 0x801f
800a0170 addu   $at, $v1
800a0174 sb     $v0, -0x4932(at) ; cap it to 8
```
The code can be found at:
```
BIN/BATTLE/BATTLE.EMI: 00093840
BIN/BATTLE/BATTLE2.EMI: 00093840
BIN/BOSS/BOSS001.EMI: 00051040
BIN/BOSS/BOSS002.EMI: 00094840
BIN/BOSS/BOSS004.EMI: 00051040
BIN/BOSS/BOSS007.EMI: 00093840
BIN/BOSS/BOSS008.EMI: 00091840
BIN/BOSS/BOSS012.EMI: 00094840
BIN/BOSS/BOSS013.EMI: 00094840
BIN/BOSS/BOSS014.EMI: 00093840
BIN/BOSS/BOSS015.EMI: 00093840
BIN/BOSS/BOSS017.EMI: 00094840
BIN/BOSS/BOSS018.EMI: 00094840
BIN/BOSS/BOSS019.EMI: 00094840
BIN/BOSS/BOSS020.EMI: 00094840
BIN/BOSS/BOSS021.EMI: 00094840
BIN/BOSS/BOSS022.EMI: 00051040
BIN/BOSS/BOSS023.EMI: 00091840
BIN/BOSS/BOSS024.EMI: 00094840
BIN/BOSS/BOSS025.EMI: 00051040
BIN/BOSS/BOSS027.EMI: 00094840
BIN/BOSS/BOSS028.EMI: 00094840
BIN/BOSS/BOSS029.EMI: 00094840
BIN/BOSS/BOSS030.EMI: 00094840
BIN/BOSS/BOSS031.EMI: 00051040
BIN/BOSS/BOSS032.EMI: 00094840
BIN/BOSS/BOSS033.EMI: 00093840
BIN/BOSS/BOSS034.EMI: 00094840
BIN/BOSS/BOSS035.EMI: 00094840
BIN/BOSS/BOSS036.EMI: 00094840
BIN/BOSS/BOSS037.EMI: 00094840
BIN/BOSS/BOSS038.EMI: 00094840
BIN/BOSS/BOSS040.EMI: 00094840
BIN/BOSS/BOSS042.EMI: 00094840
BIN/BOSS/BOSS046.EMI: 00094840
BIN/BOSS/BOSS047.EMI: 00094840
BIN/BOSS/BOSS049.EMI: 00094840
BIN/BOSS/BOSS050.EMI: 00094840
BIN/BOSS/BOSS051.EMI: 00094840
BIN/BOSS/BOSS052.EMI: 00092040
BIN/BOSS/BOSS054.EMI: 00094840
BIN/BOSS/BOSS055.EMI: 00097840
```