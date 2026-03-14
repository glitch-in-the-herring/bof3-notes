| ID     |
| ------ |
| `0x19` |

| ID     |
| ------ |
| `0x1a` |
The Shaman'sRing and the Spirit Ring reduces the AP cost of any spell their wearers cast by 25% and 50% respectively. The code that does this change can be found at `SLUS_004.22: 000d0a68` in the game's files:

```
80166a68 lbu    $a1, 0x0012(a0) ; load caster's first accessory
80166a6c lui    $at, 0x801d
80166a70 addu   $at, $v0
80166a74 lbu    $v1, -0x58e6(at) ; load AP cost of the spell
80166a78 beq    $a1, $a2, 0x80166a94 ; check if the caster is wearing a Spirit Ring in the first slot
80166a7c andi   $v0, $v1, 0xffff
80166a80 lbu    $v0, 0x0013(a0) ; load caster's second accessory
80166a84 nop    
80166a88 bne    $v0, $a2, 0x80166aa0 ; check if caster is wearing a Shaman's Ring Ring in the first slot
80166a8c li     $a0, 0x0019
80166aa0 beq    $a1, $a0, 0x80166ab0  ; check if the caster is wearing a Spirit Ring in the second slot
80166aa4 nop    
80166aa8 bne    $v0, $a0, 0x80166adc ; check if the caster is wearing a Shaman'sRing in the second slot
80166aac nop    

; if the caster is wearing a Spirit Ring
80166a94 addiu  $v0, 0x0001 ; add 1 to the AP cost
80166a98 j      0x80166adc
80166a9c srl    $v1, $v0, 0x01 ; divde AP cost + 1 by 2. The + 1 to the AP cost effectively make sthis AP cost / 2, rounded up.
80166adc jr     $ra
80166ae0 andi   $v0, $v1, 0x00ff

; if the caster is wearing a Shaman's ring
80166ab0 andi   $v1, 0xffff
80166ab4 sll    $v0, $v1, 0x01 ; multiply AP cost by 2
80166ab8 addu   $v0, $v1 ; multiply AP cost by 3
80166abc move   $v1, $v0
80166ac0 andi   $v0, 0x0003
80166ac4 beqz   $v0, 0x80166ad8 ; check if AP cost * 3 is divisible by 4
80166ac8 andi   $v0, $v1, 0xffff

    ; if AP cost is not divisible by 4
    80166ac4 beqz   $v0, 0x80166ad8
    80166ac8 andi   $v0, $v1, 0xffff
    80166acc srl    $v0, 0x02 ; divide AP cost * 3 by 4
    80166ad0 j      0x80166adc
    80166ad4 addiu  $v1, $v0, 0x0001 ; add 1 to AP cost * 3 / 4, this effectively round the division up


    ; if AP  cost * 3 is divisible by 4
    80166ad8 srl    $v1, $v0, 0x02 ; divide AP cost * 3 by 4
    80166adc jr     $ra
    80166ae0 andi   $v0, $v1, 0x00ff
    801d3518 j      0x801d3560
    801d351c nop    
    801d3560 lui    $at, 0x8014
    801d3564 sb     $v0, 0x63c8(at) ; store new AP cost
```