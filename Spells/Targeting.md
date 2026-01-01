The available targeting options are:

| Byte   | Targeting                                  | Field | First Target | Example                         | Notes                                                                                       |
| ------ | ------------------------------------------ | ----- | ------------ | ------------------------------- | ------------------------------------------------------------------------------------------- |
| `0x02` | Self                                       | False | Player part  | Accession                       | The only spells that use this targeting option are Main Cannon, Accession, and Restore Form |
| `0x0e` | Self                                       | False | Player party | Focus                           |                                                                                             |
| `0x1e` | All<br>Always player party                 | False | Player party | War Shout                       |                                                                                             |
| `0x1f` | All<br>Always player party                 | True  | Player party | [[Noting#Noting 11\|Noting 11]] | Noting 11 is the only spell that uses this targeting option                                 |
| `0x32` | All<br>Always enemy party                  | False | Enemy party  | Ragnarok                        |                                                                                             |
| `0x3a` | All<br>Always enemy party                  | False | Enemy party  | Kyrie                           |                                                                                             |
| `0x3e` | All<br>Always enemy party                  | False | Enemy party  | Sleep                           | Sleep is the only spell that uses this targeting option                                     |
| `0x4e` | Single<br>Always player party              | False | Player party | Raise Dead                      |                                                                                             |
| `0x62` | Single<br>Always enemy party               | False | Enemy party  | Mind Sword                      |                                                                                             |
| `0x6a` | Single<br>Always enemy party               | False | Enemy party  | Blind                           |                                                                                             |
| `0x6e` | Single<br>Always enemy party               | False | Enemy party  | Identify                        |                                                                                             |
| `0x7a` | All?<br>Always enemy party?                | False | Enemy party? | [[Noting#Noting 8\|Noting 8]]   | Noting 8 is the only spell that uses this targeting option. Conjectural.                    |
| `0x7e` | All<br>Always enemy party                  | False | Enemy party  | Silence                         |                                                                                             |
| `0x96` | All<br>Player and enemy party              | False | ?            | Sanctuary                       | Sanctuary is the only spell that uses this targeting option                                 |
| `0x9e` | All? (random)<br>Player and enemy party    | False | ?            | SuddenDeath                     | SuddenDeath is the only spell that uses this targeting option                               |
| `0xba` | Single? (random)<br>Player and enemy party | False | ?            | Tornado                         | Tornado is the only spell that uses this targeting option                                   |
| `0xce` | Single<br>Player or enemy party            | False | Player party | Protect                         |                                                                                             |
| `0xcf` | Single<br>Player or enemy party            | True  | Player party | Purify                          |                                                                                             |
| `0xde` | All<br>Player or enemy party               | False | Player party | Shield                          |                                                                                             |
| `0xdf` | All<br>Player or enemy party               | True  | Player party | Vitalize                        |                                                                                             |
| `0xe2` | Single<br>Player or enemy party            | False | Enemy party  | Myollnir                        |                                                                                             |
| `0xea` | Single<br>Player or enemy party            | False | Enemy party  | FlameStrike                     |                                                                                             |
| `0xee` | Single<br>Player or enemy party            | False | Enemy party  | Slow                            |                                                                                             |
| `0xf2` | All<br>Player or enemy party               | False | Enemy party  | Inferno                         |                                                                                             |
Terminology:

| Term                   | Meaning                                                                               |
| ---------------------- | ------------------------------------------------------------------------------------- |
| Player or enemy party  | The user can make a choice between targets in the enemy's party or the player's party |
| Player and enemy party | Every single member of both the player and enemy party are targeted                   |
As bit switches (still tentative):

| Bit    | Function            | Notes |
| ------ | ------------------- | ----- |
| `0x01` | Usable in the field |       |
| `0x10` | Target all          |       |

