| ID     |
| ------ |
| `0x03` |
The Speed Boots increases the wearer's AGL by 10.
```
80165be4 addiu  $a0, $s0, 0x0008 ; load the location for AGL
80165be8 jal    0x801654f4 ; call the stat change function
80165bec li     $a1, 0x000a ; set the change to 0
```
The code can be found at `SLUS_004.22: 000cfbe4`