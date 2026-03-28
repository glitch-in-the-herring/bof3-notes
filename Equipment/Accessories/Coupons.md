| ID     |
| ------ |
| `0x1b` |
Coupons give a 20% discount on all stores. It cannot be stacked with the [[Flyer]].
```
801d357c li     $s2, 0x001b ; load Coupon's ID
801d3580 sw     $ra, 0x001c(sp)
801d3584 sh     $v0, 0x0000(s1)
801d3588 jal    0x801bdb7c
801d358c move   $a0, $r0
    801bdb7c move   $a1, $r0
    801bdb80 li     $a2, 0x00ff
    801bdb84 andi   $a0, 0x00ff
    801bdb88 lui    $v1, 0x8014
    801bdb8c addiu  $v1, 0x4f5a
    801bdb90 sll    $v0, $a0, 0x01
    801bdb94 addu   $v0, $a0
    801bdb98 addu   $v1, $v0, $v1
        801bdb9c lbu    $v0, 0x0000(v1) ; check if the party member slot is empty
        801bdba0 nop    
        801bdba4 beq    $v0, $a2, 0x801bdbbc
        801bdba8 nop    
        801bdbac addiu  $a1, 0x0001 ; add the party member counter
        801bdbb0 slti   $v0, $a1, 0x0003
        801bdbb4 bnez   $v0, 0x801bdb9c ; loop three times
        801bdbb8 addiu  $v1, 0x0001
    801bdbbc jr     $ra
    801bdbc0 andi   $v0, $a1, 0x00ff
    801d3590 andi   $v1, $s0, 0x00ff
    801d3594 andi   $v0, 0x00ff
    801d3598 sltu   $v0, $v1, $v0
    801d359c beqz   $v0, 0x801d3604
    801d35a0 sll    $v0, $v1, 0x02
    801d35a4 addu   $v0, $v1
    801d35a8 sll    $v0, 0x06
    801d35ac lui    $at, 0x8014
    801d35b0 addu   $at, $v0
    801d35b4 lbu    $v1, 0x5fcc(at)
    801d35b8 nop    
    801d35bc sll    $v0, $v1, 0x02
    801d35c0 addu   $v0, $v1
    801d35c4 sll    $v0, 0x03
    801d35c8 addu   $v0, $v1
    801d35cc sll    $v0, 0x02
    801d35d0 lui    $v1, 0x8014
    801d35d4 addiu  $v1, 0x4968
    801d35d8 addu   $v1, $v0, $v1
    801d35dc lbu    $v0, 0x0012(v1) ; load the character's first accessory
    801d35e0 nop    
    801d35e4 beq    $v0, $s2, 0x801d3600
    801d35e8 li     $v0, 0x0050
    801d35ec lbu    $v0, 0x0013(v1) ; load the character's second accessory
    801d35f0 nop    
    801d35f4 bne    $v0, $s2, 0x801d3588 ; loop until the counter runs out or the Coupon is found
    801d35f8 addiu  $s0, 0x0001 ; increment the counter
    801d3588 jal    0x801bdb7c
    801d358c move   $a0, $r0
; if the Coupon is found
801d35fc li     $v0, 0x0050 ; load the new price percentage
801d3600 sh     $v0, 0x0000(s1) ; store the price percentage
```
The code can be found at `BIN/ETC/SHOP.EMI: 0000317c`.