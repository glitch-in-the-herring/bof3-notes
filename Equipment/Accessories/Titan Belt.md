| ID     |
| ------ |
| `0x01` |
The Titan Belt increases the wearer's PWR by 10.
```
80165bc8 j      0x80165be8
80165bcc addiu  $a0, $s0, 0x0004 ; load the location for PWR
80165be8 jal    0x801654f4 ; call the stat change function
80165bec li     $a1, 0x000a ; set the change to 10 
```
This can be found at `SLUS_004.22: 000cfbc8`