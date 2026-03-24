The code that changes the stats consists of two parts: the context and the stat changer. The stat changer is the same for all of these:

```
801654f4 lhu    $v1, 0x0000(a0) ; load the stat
801654f8 sll    $v0, $a1, 0x10
801654fc sra    $v0, 0x10
80165500 blez   $v0, 0x80165534
80165504 li     $a2, 0x03e7

; if the stat change is negative
80165534 bgez   $v0, 0x80165564
80165538 nop    
8016553c beqz   $v1, 0x80165564 

; if the current stat is not zero
80165540 addu   $v0, $v1, $a1 ; add the stat change to the stat
80165544 sh     $v0, 0x0000(a0) ; store the new atat
80165548 sll    $v0, 0x10
8016554c bgez   $v0, 0x80165564
80165550 subu   $v0, $r0, $v1
80165564 move   $v0, $r0
80165568 jr     $ra
8016556c nop    
```
This code can be found at `SLUS_004.22: 000cf4f4`.
Stats that cap at 100 use this formula instead:
```
80165694 lbu    $a2, 0x0000(a0) ; load the stat
80165698 li     $v0, 0x0064
8016569c andi   $v1, $a2, 0x00ff
801656a0 bne    $v1, $v0, 0x801656b0
801656a4 addu   $v0, $a2, $a1 ; add the stat and the stat change

; if the stat is not 100
801656b0 sb     $v0, 0x0000(a0) ; store the new stat
801656b4 sll    $v0, 0x18
801656b8 bgez   $v0, 0x801656c4
801656bc nop    
801656c4 lbu    $v0, 0x0000(a0) ; load the changed stat
801656c8 nop    
801656cc sltiu  $v0, 0x0065
801656d0 bnez   $v0, 0x801656e4
801656d4 li     $v0, 0x0001

; if tje changed stat is less than or equal to 100
801656e4 jr     $ra
801656e8 nop    
```
This code can be found at `SLUS_004.22: 000cf694`.