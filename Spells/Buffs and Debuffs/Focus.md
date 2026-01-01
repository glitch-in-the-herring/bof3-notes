| Spell ID         | Targeting     | Power | AP  | Element | Battle Spell Call |
| ---------------- | ------------- | ----- | --- | ------- | ----------------- |
| `0x27`<br>39<br> | `0xe`<br>Self | 50*   | 0   |         | `0x6c`            |
\* Unused
Focus increments the focus counter by 1, up to a maximum of 2. It is reset to 0 if in the turn after Focus is cast, the caster does not use a melee attack. The counter gives a bonus to the PWR when using the [[Melee Formula]], which is not capped to 999 like normal.
```
800a1524 lbu    $v1, 0x5fc8(at) ; load current focus counter
800a1528 nop    
800a152c sltiu  $v0, $v1, 0x0002 ; cap to 2
800a1530 beqz   $v0, 0x800a15cc

; if the counter is less than 2
800a1534 addiu  $v0, $v1, 0x0001 ; add 1 to focus counter
800a1538 lui    $at, 0x8014
800a153c addu   $at, $a0
800a1540 sb     $v0, 0x5fc8(at) ; store new focus counter
```