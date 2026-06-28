Accessory calls are functions that are called by accessories when they are equipped.
```
80165b98 lbu    $v0, 0x0000(s1) ; load accessory ID
80165b9c nop    
80165ba0 addiu  $v1, $v0, -0x0001 ; subtract the ID by 1 to get the index
80165ba4 sltiu  $v0, $v1, 0x0017
80165ba8 beqz   $v0, 0x80165d18
; if the accessory ID is not zero
80165bac sll    $v0, $v1, 0x02 ; multiply the index by 4
80165bb0 lui    $at, 0x8015
80165bb4 addu   $at, $v0 ; add offset to base address
80165bb8 lw     $v0, -0x6138(at) ; load the accessory call's address
80165bbc nop    
80165bc0 jr     $v0 ; execute the accessory call
80165bc4 nop    
```
This code can be found at `SLUS_004.22: 000cfb98`
The table for accessory calls can be found at `SLUS_004.22: 000b3ec8`.
## Calls
