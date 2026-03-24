The inventory taker is a function that subtracts a given amount from the quantity of a specified item given by its ID. It returns 1 if the item quantity was successfully reduced and 0 if the item was not found or if there are not enough items.

| `$a0` | [[Inventory#Inventory Type\|Inventory type ID]] |
| ----- | ----------------------------------------------- |
| `$a1` | Item ID                                         |
| `$a2` | Quantity to take                                |
```
801665a0 andi   $a1, 0x00ff
801665a4 beqz   $a1, 0x80166634 ; check item ID
801665a8 move   $v0, $r0
; if the item ID is not zero
801665ac andi   $a3, $a2, 0x00ff
801665b0 beqz   $a3, 0x80166630
801665b4 andi   $v0, $a0, 0x00ff
; if the quantity to take is not zero
801665b8 move   $v1, $r0
801665bc move   $t0, $a3
801665c0 sll    $v0, 0x02
801665c4 lui    $at, 0x801d
801665c8 addu   $at, $v0
801665cc lw     $a3, -0x76c4(at) ; load the base item ID address
801665d0 lui    $at, 0x801d
801665d4 addu   $at, $v0
801665d8 lw     $a0, -0x76b0(at) ; load the base item quantity address
    ; loop until the item ID is either found or the counter runs out
    801665dc lbu    $v0, 0x0000(a3) ; load the current item ID
    801665e0 nop    
    801665e4 bne    $v0, $a1, 0x8016661c ; check if the current item matches the desried item ID
    801665e8 addiu  $v1, 0x0001 ; add 1 to the counter
    8016661c addiu  $a3, 0x0001 ; move to the next item ID
    80166620 andi   $v0, $v1, 0x00ff
    80166624 sltiu  $v0, 0x0080
    80166628 bnez   $v0, 0x801665dc ; loop if the counter is still below 128
    8016662c addiu  $a0, 0x0001 ;  move to the next item quantity
; if the item was found
801665ec lbu    $v1, 0x0000(a0) ; load the current item quantity
801665f0 nop    
801665f4 sltu   $v0, $v1, $t0 ; check the amount
801665f8 bnez   $v0, 0x80166634
; if the current quantity is less than the requested amount
801665fc move   $v0, $r0 ; return 0
; if the item was not found
80166630 move   $v0, $r0 ; return 0
80166634 jr     $ra
; if the current quantity is greater than the requested amount
80166600 subu   $v0, $v1, $a2 ; subtract the current quantity by the requested quantity
80166604 sb     $v0, 0x0000(a0) ; store the new quantity
80166608 andi   $v0, 0x00ff
8016660c bnez   $v0, 0x80166634 
80166610 li     $v0, 0x0001 ; set 1 as the return value
; if the new quantity is zero
80166614 j      0x80166634
80166618 sb     $r0, 0x0000(a3) ; set the item ID to zero
; if the new quantity is greater than 0
80166634 jr     $ra
80166638 nop    
```
This code can be found at `SLUS_004.22: 000d05a0`
