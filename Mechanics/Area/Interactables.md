## Format
There are ... types of interactables:

| ID     | Interactable     | Section size |
| ------ | ---------------- | ------------ |
| `0x00` | Chrysm           | 15           |
| `0x10` | NPC              | 16           |
| `0x70` | Fightable? NPCs? | 15           |
| `0x90` | Chests and items | 13           |

The size of the sections can be found at:
* `0x801c8444` in the RAM
## Types
### Chrysm

| Position | Description          |
| -------- | -------------------- |
| 0        | Interactable type    |
| 7        | x-axis position      |
| 9        | y-axis position      |
| 10       | Pathfinding behavior |

### NPCs
| Position | Description          |
| -------- | -------------------- |
| 0        | Interactable type    |
| 7        | x-axis position      |
| 9        | y-axis position      |
| 10       | Pathfinding behavior |
| 15       | Dialogue index       |

### Item Container

| Position | Description       |
| -------- | ----------------- |
| 0        | Interactable type |
| 2        | Container type    |
| 5        | y-axis position   |
| 6        | ?                 |
| 7        | x-axis position   |
| 8        | Flag index        |
| 9        | Item ID           |
| 10       | Item type         |
| 11       | Rotation          |
| 12       |                   |

The container types are:

| ID     | Type           |
| ------ | -------------- |
| `0x4b` | Treasure chest |
| `0x4f` | Sack           |
## Pathfinding Behaviour

| Bit    | Type          |
| ------ | ------------- |
| `0x00` | Random?       |
| `0x01` | Avoid player  |
| `0x02` | Follow player |
| `0x04` | Static?       |
| `0x08` | Hovering?     |
