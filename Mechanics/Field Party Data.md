Field Party data is located at:
* `0x80144968` in the RAM
* in the save file
This data gets copied to the [[Combatant Data (Player)|player combatant data]] when entering a battle and when entering the world map.

| Position | Description           | Value(s)                     | Note                                                                                                                         |
| -------- | --------------------- | ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 0-4      | Name                  | ASCII null-terminated string |                                                                                                                              |
| 5        | Character ID          | 8-bit unsigned integer       | See [[Ordering]]                                                                                                             |
| 6        | Level                 | 8-bit unsigned integer       |                                                                                                                              |
| 8-11     | EXP                   | 32-bit unsigned integer      |                                                                                                                              |
| 12-13    | Status                | See [[Status]]               |                                                                                                                              |
| 14       | Weapon                | 8-bit unsigned integer       |                                                                                                                              |
| 15       | Shield                | 8-bit unsigned integer       |                                                                                                                              |
| 16       | Helmet                | 8-bit unsigned integer       |                                                                                                                              |
| 17       | Chestplate            | 8-bit unsigned integer       |                                                                                                                              |
| 18       | Accessory 1           | 8-bit unsigned integer       |                                                                                                                              |
| 19       | Accessory 2           | 8-bit unsigned integer       |                                                                                                                              |
| 20-21    | Current HP            | 16-bit unsigned integer      |                                                                                                                              |
| 22-23    | Current AP            | 16-bit unsigned integer      |                                                                                                                              |
| 27       | Master                | 8-bit unsigned integer       |                                                                                                                              |
| 28-29    | Current Max HP        | 16-bit unsigned integer      |                                                                                                                              |
| 30-31    | Current Max AP        | 16-bit unsigned integer      |                                                                                                                              |
| 32-33    | Effective PWR         | 16-bit unsigned integer      | This is the combatant's PWR after all equipment modifiers and buffs/debuffs.                                                 |
| 34-35    | Effective DEF         | 16-bit unsigned integer      | This is the combatant's DEF after all equipment modifiers and buffs/debuffs.                                                 |
| 36-37    | Effective AGL         | 16-bit unsigned integer      | This is the combatant's AGL after all equipment modifiers and buffs/debuffs.                                                 |
| 38-39    | Effective INT         | 16-bit unsigned integer      | This is the combatant's INT after all equipment modifiers and buffs/debuffs.                                                 |
| 42       | Effective Willpower   | 8-bit unsigned integer       |                                                                                                                              |
| 43-51    | Effective resistances | 8-bit unsigned integers      | This is the combatant's resistances after all equipment modifiers.<br>See [[Resistance]] for the order of resistances.       |
| 52       | Effective surprise    | 8-bit unsinged integer       |                                                                                                                              |
| 53       | Effective reprisal    | 8-bit unsinged integer       |                                                                                                                              |
| 54       | Effective critical    | 8-bit unsinged integer       |                                                                                                                              |
| 55       | Effective dodge       | 8-bit unsinged integer       |                                                                                                                              |
| 56       | Effective accuracy    | 8-bit unsinged integer       |                                                                                                                              |
| 60-61    | True Max HP           | 16-bit unsigned integer      |                                                                                                                              |
| 62-63    | True Max AP           | 16-bit unsigned integer      |                                                                                                                              |
| 64-65    | Base PWR              | 16-bit unsigned integer      | This is the combatant's PWR without any non-permanent modifiers.                                                             |
| 66-67    | Base DEF              | 16-bit unsigned integer      | This is the combatant's DEF without any non-permanent modifiers.                                                             |
| 68-69    | Base AGL              | 16-bit unsigned integer      | This is the combatant's AGL without any non-permanent modifiers.                                                             |
| 70-71    | Base INT              | 16-bit unsigned integer      | This is the combatant's INT without any non-permanent modifiers.                                                             |
| 74       | Base Willpower        | 8-bit unsigned integer       |                                                                                                                              |
| 75-83    | Base resistances      | 8-bit unsigned integers      | This is the combatant's resistances without any non-permanent modifiers.<br>See [[Resistance]] for the order of resistances. |
| 84       | Base surprise         | 8-bit unsinged integer       |                                                                                                                              |
| 85       | Base reprisal         | 8-bit unsinged integer       |                                                                                                                              |
| 86       | Base critical         | 8-bit unsinged integer       |                                                                                                                              |
| 87       | Base dodge            | 8-bit unsinged integer       |                                                                                                                              |
| 88       | Base accuracy         | 8-bit unsinged integer       |                                                                                                                              |
| 92-101   | Heal spells           | 8-bit unsigned integers      |                                                                                                                              |
| 102-111  | Assist spells         | 8-bit unsigned integers      |                                                                                                                              |
| 112-121  | Attack spells         | 8-bit unsigned integers      |                                                                                                                              |
| 122-131  | Skills                | 8-bit unsigned integers      |                                                                                                                              |
| 132      | Apprenticing level    | 8-bit unsigned integer       |                                                                                                                              |
| 133      | HP growth             | 8-bit signed integer         |                                                                                                                              |
| 134      | AP growth             | 8-bit signed integer         |                                                                                                                              |
| 135      | PWR growth            | 8-bit signed integer         |                                                                                                                              |
| 136      | DEF growth            | 8-bit signed integer         |                                                                                                                              |
| 137      | AGL growth            | 8-bit signed integer         |                                                                                                                              |
| 138      | INT growth            | 8-bit signed integer         |                                                                                                                              |
