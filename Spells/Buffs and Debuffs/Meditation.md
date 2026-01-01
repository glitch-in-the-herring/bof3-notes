| Spell ID          | Targeting     | Power | AP  | Element | Battle Spell Call |
| ----------------- | ------------- | ----- | --- | ------- | ----------------- |
| `0xa3`<br>163<br> | `0xe`<br>Self | 50*   | 0   |         | `0x6d`            |
\* Unused
Meditation increments the meditation counter by 1, up to a maximum of 2. It is reset to 0 if in the turn after Meditation is cast, the caster does not use an ability. The counter gives a bonus to the INT when using the [[Magic Formula]], which is not capped to 999 like normal.
```
800a164c lbu    $v1, 0x5fc9(at) ; load current meditation counter
800a1650 nop    
800a1654 sltiu  $v0, $v1, 0x0002 ; cap to 2
800a1658 beqz   $v0, 0x800a16f4

; if the counter is less than 2
800a165c addiu  $v0, $v1, 0x0001 ; add 1 to the meditation counter
800a1660 lui    $at, 0x8014
800a1664 addu   $at, $a0
800a1668 sb     $v0, 0x5fc9(at) ; store new meditation counter
```