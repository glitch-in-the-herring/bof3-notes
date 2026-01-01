| Spell ID     | Targeting     | Power | AP  | Element | Battle Spell Call |
| ------------ | ------------- | ----- | --- | ------- | ----------------- |
| `0x3e`<br>62 | `0xe`<br>Self | 50    | 0   |         | `0x00`            |
Celerity adds its spell power value to all of the caster's [[Stat Multiplier|stat multipliers]], capped to 100. This cap is different from the other buff spells.
```
801ef3c4 slti   $v0, $v1, 0x0065 ; check if greater than 100
801ef3c8 bnez   $v0, 0x801ef3dc
801ef3cc slti   $v0, $v1, -0x0064 ; cap if less than -100
801ef3d0 li     $v0, 0x0064

; if greater than 100 
801ef3d4 j      0x801ef404
801ef3d8 sb     $v0, 0x0014(a0) ; cap to 100


801ef3dc beqz   $v0, 0x801ef3ec
801ef3e0 li     $v0, -0x0064
801ef3e4 j      0x801ef404
801ef3e8 sb     $v0, 0x0014(a0) ; cap to -100
```
Once used, it starts the countdown timer at `0x80145554`, which is formatted as such:

| Position | Value                                              |
| -------- | -------------------------------------------------- |
| 0        | Hour                                               |
| 1        | Minute                                             |
| 2        | Second                                             |
| 3        | Subsecond (by default this is 1/30ths of a second) |
By default, it waits for five hours:
```
801ef2bc li     $a0, 0x0005 ; load hour
...
801ef2d0 sb     $a0, 0x5554(at) ; store hour
```
For as long as this time is not zero, then the spell cannot be used again.