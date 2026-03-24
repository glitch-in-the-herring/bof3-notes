| ID     |
| ------ |
| `0x02` |
The High Boots increases the wearer's DEF by 5.
```
80165bd0 addiu  $a0, $s0, 0x0006 ; load the location for DEF
80165bd4 jal    0x801654f4 ; call the stat change function
80165bd8 li     $a1, 0x0005 ; set the change to 5
```
This can be found at `SLUS_004.22: 000cfbd0`