All of the elemental rings use the [[resistance to 7]] code.
## Ring of Ice

| ID     |
| ------ |
| `0x0a` |

The Ring of Ice raises the user's ice resistance to 7
```
80165c20 addiu  $a0, $s0, 0x0010 ; offset for ice resistance
```
## Ring of Fire
| ID     |
| ------ |
| `0x0b` |

The Ring of Fire raises the user's fire resistance to 7
```
80165c2c addiu  $a0, $s0, 0x000f ; offset for fire resistance
```
## Thunder Ring
| ID     |
| ------ |
| `0x0c` |

The Thunder Ring raises the user's thunder resistance to 7
```
80165c38 addiu  $a0, $s0, 0x0011 ; offset for thunder resistance
```
The code can be found at `/SLUS_004.22: 000cfc20` beginning with the code for the Ring of Ice