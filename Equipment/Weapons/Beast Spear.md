The Beast Spear drains 5% of the user's max HP
```
801d5f70 lbu    $v1, 0x5f12(at) ; load weapon's ID
801d5f74 li     $v0, 0x0052 ; load the ID of the Beast Spear
801d5f78 bne    $v1, $v0, 0x801d5ff4
801d5f7c andi   $a0, $s1, 0x00ff
; if the weapon is a Beast Spear
801d5f80 lui    $at, 0x8014
801d5f84 addu   $at, $a1
801d5f88 lhu    $v1, 0x5f20(at) ; load the character's current max HP
801d5f8c nop    
801d5f90 addiu  $v1, 0x000a ; add 10 to the current max HP
801d5f94 mult   $v1, $s2
801d5f98 lui    $at, 0x8014
801d5f9c addu   $at, $a1
801d5fa0 lhu    $v0, 0x5fac(at)
801d5fa4 sra    $v1, 0x1f
801d5fa8 mfhi   $a2, $hi
801d5fac sra    $a0, $a2, 0x03 ; multiply the current max HP by 5%
801d5fb0 subu   $a0, $v1
801d5fb4 addu   $v0, $a0
801d5fb8 lui    $at, 0x8014
801d5fbc addu   $at, $a1
801d5fc0 sh     $v0, 0x5fac(at) ; store the HP change
```