The resistance to 7 function sets a character's specified resistance to 7. The address of the resistance must be provided to the first argument register (`$a0`).
```
80165668 lbu    $v0, 0x0000(a0) ; load current resistance
8016566c nop    
80165670 sltiu  $v0, 0x0007 ; check if the resistance is less than 7
80165674 beqz   $v0, 0x80165688

; If the current resistance is less than 7
80165678 li     $v0, 0x0007
8016567c sb     $v0, 0x0000(a0) ; set the resistance to 7
```
The code can be found at `SLUS_004.22: 000cf668`.