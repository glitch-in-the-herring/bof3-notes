The clock is a data structure in the game that is used to count time. It consists of four bytes:

| Position | Value                                              |
| -------- | -------------------------------------------------- |
| 0        | Hour                                               |
| 1        | Minute                                             |
| 2        | Second                                             |
| 3        | Subsecond (by default this is 1/30ths of a second) |
All of the fields are treated as unsigned. 

