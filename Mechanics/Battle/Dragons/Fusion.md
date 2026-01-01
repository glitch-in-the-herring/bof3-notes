## Peco
The super form of the Peco hybrid has innate regen. 1/20 of the hybrid's (max HP + 10) is regenerated every turn.
```
801d5f1c lhu    $v1(00000000), 0x5f20(at)([80145f20] = 095b) ; load current max HP
801d5f20 nop    
801d5f24 addiu  $v1(0000095b), 0x000a
801d5f28 mult   $v1(00000965), $s2(66666667) ; divide by 20
801d5f2c lui    $at(80140000), 0x8014
801d5f30 addu   $at(80140000), $a1(00000000)
801d5f34 lhu    $v0(00000012), 0x5fac(at)([80145fac] = 0005) ; load any existing HP changes
801d5f38 sra    $v1(00000965), 0x1f
801d5f3c mfhi   $a2(00000000), $hi(000003c2)
801d5f40 sra    $a0(00000000), $a2(000003c2), 0x03
801d5f44 subu   $a0(00000078), $v1(00000000)
801d5f48 subu   $v0(00000005), $a0(00000078) 
801d5f4c lui    $at(80140000), 0x8014
801d5f50 addu   $at(80140000), $a1(00000000)
801d5f54 sh     $v0(ffffff8d), 0x5fac(at)([80145fac] = 0005) ; store regen
```