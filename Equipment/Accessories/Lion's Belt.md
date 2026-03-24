| ID     |
| ------ |
| `0x05` |
The Lion's Belt increases the wearer's willpower by 10.
```
80165c0c addiu  $a0, $s0, 0x000e ; load the location for willpower
80165c10 jal    0x801654b0 ; call the stat change function
80165c14 li     $a1, 0x000a ; set the change to 10
```
This can be found at `SLUS_004.22: 000cfc0c`