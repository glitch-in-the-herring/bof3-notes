| ID     |
| ------ |
| `0x01` |
The flyer is an item that gives a 30% discount on items sold in the Arena. It does not stack with [[Coupons]].
```
801d3604 jal    0x80166140 ; call the vital items checker
801d3608 li     $a0, 0x0001 ; load Flyer's ID
801d360c andi   $v0, 0x00ff
801d3610 beqz   $v0, 0x801d3638
801d3614 nop    
; if the Flyer exists in the inventory
801d3618 lui    $v0, 0x8015
801d361c lbu    $v0, -0x7967(v0)
801d3620 nop    
801d3624 addiu  $v0, -0x0006
801d3628 sltiu  $v0, 0x0002
801d362c beqz   $v0, 0x801d3638
801d3630 li     $v0, 0x0046 ; load the new price percentage
801d3634 sh     $v0, 0x0000(s1) ; store the price percentage
```
This code can be found at `BIN/ETC/SHOP.EMI: 00003204`