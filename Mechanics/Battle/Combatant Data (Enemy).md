The enemy party's combatant data starts at `0x801eb630` in the RAM and is 320 bytes long for each combatant.

| Position | Description           | Value(s)                     | Note                                                                                                             |
| -------- | --------------------- | ---------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| 5        | Combatant ID          | 8-bit unsigned integer       |                                                                                                                  |
| 116-119  | Name                  | ASCII null-terminated string |                                                                                                                  |
| 148-149  | Current HP            | 16-bit signed integer        |                                                                                                                  |
| 150-151  | Current AP            | 16-bit signed integer        |                                                                                                                  |
| 152      | Steal item ID         | 8-bit unsigned integer       |                                                                                                                  |
| 153      | Steal item type       | 8-bit unsigned integer       |                                                                                                                  |
| 154      | Steal rate            | 8-bit unsigned integer       |                                                                                                                  |
| 155      | Steal item charm flag | 8-bit unsigned integer       |                                                                                                                  |
| 156      | Drop item ID          | 8-bit unsigned integer       |                                                                                                                  |
| 157      | Drop item type        | 8-bit unsigned integer       |                                                                                                                  |
| 158      | Drop rate             | 8-bit unsigned integer       |                                                                                                                  |
| 159      | Drop item charm flag  | 8-bit unsigned integer       |                                                                                                                  |
| 160-161  | Current max HP        | 16-bit signed integer        |                                                                                                                  |
| 162-163  | Current max AP        | 16-bit signed integer        |                                                                                                                  |
| 164-165  | Effective PWR         | 16-bit unsigned integer      |                                                                                                                  |
| 166-167  | Effective DEF         | 16-bit unsigned integer      |                                                                                                                  |
| 168-169  | Effective AGL         | 16-bit unsigned integer      |                                                                                                                  |
| 170-171  | Effective INT         | 16-bit unsigned integer      |                                                                                                                  |
| 175-183  | Effective resistances | 8-bit unsigned integers      | This is the combatant's resistances after all buffs/debuffs.<br>See [[Resistance]] for the order of resistances. |
| 192-193  | True max HP           | 16-bit unsigned integer      |                                                                                                                  |
| 194-195  | True max AP           | 16-bit unsigned integer      |                                                                                                                  |
| 196-197  | Base PWR?             | 16-bit unsigned integer      |                                                                                                                  |
| 198-199  | Base DEF?             | 16-bit unsigned integer      |                                                                                                                  |
| 200-201  | Base AGL?             | 16-bit unsigned integer      |                                                                                                                  |
| 202-203  | Base INT?             | 16-bit unsigned integer      |                                                                                                                  |
| 207-215  | Base resistances?     | 8-bit unsigned integers      |                                                                                                                  |
| 248-249  | HP change             | 16-bit signed integer        | See [[HP-AP Change]]                                                                                             |
| 250-251  | AP change             | 16-bit signed integer        | See [[HP-AP Change]]                                                                                             |
| 252      | Heal status           | 8-bit unsigned integer       | See [[HP-AP Change]]                                                                                             |
| 264      | PWR multiplier        | 8-bit signed integer         | See [[Stat Multiplier]]                                                                                          |
| 265      | DEF multiplier        | 8-bit signed integer         | See [[Stat Multiplier]]                                                                                          |
| 266      | AGL multiplier        | 8-bit signed integer         | See [[Stat Multiplier]]                                                                                          |
| 267      | INT multiplier        | 8-bit signed integer         | See [[Stat Multiplier]]                                                                                          |