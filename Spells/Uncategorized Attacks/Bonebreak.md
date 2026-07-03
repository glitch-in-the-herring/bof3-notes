| Spell ID     | Targeting                              | Power | AP  | Element | Battle Spell Call |
| ------------ | -------------------------------------- | ----- | --- | ------- | ----------------- |
| `0x15`<br>21 | `0x6a`<br>Single<br>Always enemy party | 0     | 0   |         | `0x00`            |
Bonebreak uses the [[Melee Formula]] but with the target's defense ignored. Once used, it starts the countdown timer at `0x80145558`, which uses the [[Clock]] data structure.
By default, it waits for five hours:
```
8009f73c li     $v0, 0x0005 ; load hour
8009f740 lui    $at, 0x8014
8009f744 sb     $v0, 0x5558(at) ; store hour
```
For as long as this time is not zero, then the spell cannot be used again.