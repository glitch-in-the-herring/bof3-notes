The inventory checker is a function that returns the quantity of an item given its ID. If the player does not have the item it returns zero.

| Input | Description                                     |
| ----- | ----------------------------------------------- |
| `$a0` | [[Inventory#Inventory Type\|Inventory type ID]] |
| `$a1` | Item ID                                         |
| `$a2` | Unknown                                         |

```
8016628c andi   $a2, 0x00ff
80166290 bnez   $a2, 0x801662f8
80166294 move   $a2, $r0 ; uncertain what this means
80166298 move   $a3, $r0
8016629c andi   $a1, 0x00ff
801662a0 andi   $v0, $a0, 0x00ff
801662a4 sll    $v0, 0x02 ; multiply the inventory type ID by 2
801662a8 lui    $at, 0x801d
801662ac addu   $at, $v0
801662b0 lw     $v1, -0x76c4(at) ; load the base item ID address
801662b4 lui    $at, 0x801d
801662b8 addu   $at, $v0
801662bc lw     $a0, -0x76b0(at) ; load the base quantity address
    ; loop until the item ID is either found or the counter runs out
    801662c0 lbu    $v0, 0x0000(v1) ; load the current item ID
    801662c4 nop    
    801662c8 beq    $a1, $v0, 0x801662ec ; check if the current item matches the desried item ID
    801662cc addiu  $v1, 0x0001 ; move to the next item ID
    801662d0 addiu  $a3, 0x0001 ; add 1 to the counter
    801662d4 andi   $v0, $a3, 0x00ff
    801662d8 sltiu  $v0, 0x0080 
    801662dc bnez   $v0, 0x801662c0 ; loop if the counter is still below 128
    801662e0 addiu  $a0, 0x0001 ; move to the next item quantity
; if the item was found
801662ec lbu    $v0, 0x0000(a0) ; load the current item's quantity and return it
801662f0 j      0x80166430
801662f4 nop    
80166430 jr     $ra
80166434 nop    
; if the item was not found
801662e4 j      0x80166430
801662e8 move   $v0, $r0 ; set the return value to 0
80166430 jr     $ra
80166434 nop    
```
This code can be found at `SLUS_004.22: 000d028c`.