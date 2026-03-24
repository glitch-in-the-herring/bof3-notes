| ID     |
| ------ |
| `0x04` |
The Wisdom Ring increases the wearer's INT by 30.
```
80165bf8 addiu  $a0, $s0, 0x000a ; load the location for INT
80165bfc jal    0x801654f4 ; call the stat change
80165c00 li     $a1, 0x001e ; set the change to 30
```
This can be found at `SLUS_004.22: 000cfbf8`