A party member or a combatant can be afflicted with a status effect.

| Bit    | Status     | Effects                                            |
| ------ | ---------- | -------------------------------------------------- |
| `0x04` | Paralyzed? | Skips the character's turn                         |
| `0x08` | Blind      |                                                    |
| `0x10` | Mute       | Cannot use certain abilities                       |
| `0x20` | Confused   | Cannot be controlled by the player                 |
| `0x40` | Sleeping   | Skips the character's turn, will eventually revert |
| `0x80` | Poisoned   | Drains (current HP + 5)/4 HP every turn            |
## Poisoned
### Battle
### Field
A poisoned party member loses 1 HP every ten steps:
```
801c3498 jal    0x8016813c ; go to the HP chnage function
801c349c li     $a0, 0x0001 ; load the HP change
...
801c34e4 li     $a1, 0x0001 ; load the number for the indicator
```
The code can be found at:
