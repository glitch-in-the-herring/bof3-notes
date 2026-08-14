## Culture
Culture increases in single increments when you enter the faerie village. Culture is stored at
* `0x801455c4` in the RAM
The battle counter for culture is stored at
* `0x801455b8` in the RAM
The number of battles required to go up to the next culture level is stored at:
* `0x801f2514` in the RAM
* In the following locations in the game's files:
```
BIN/ETC/COMMU00.EMI: 00004114
BIN/WORLD04/AREA175.EMI: 000cd914
BIN/WORLD04/AREA176.EMI: 000c8914
BIN/WORLD04/AREA177.EMI: 000c9114
BIN/WORLD04/AREA178.EMI: 000c9114
BIN/WORLD04/AREA179.EMI: 000c9114
BIN/WORLD04/AREA180.EMI: 000c9114
BIN/WORLD04/AREA181.EMI: 000c9114
BIN/WORLD04/AREA182.EMI: 000c9114
BIN/WORLD04/AREA183.EMI: 000c9914
BIN/WORLD04/AREA184.EMI: 000c9914
BIN/WORLD04/AREA185.EMI: 000c9914
```
If the number of battles elapsed is greater than or equal to the threshold for the current level-up, then the culture level goes up by one. The culture battle counter is set to the previous battle counter + threshold, which means that any excess battles are carried over to the next visit and are not wasted.
## Jobs
The progress for unlocked jobs is located at
* `0x801455c3` in the RAM

| Progress | New Job  |
| -------- | -------- |
| `0x01`   | Scholar  |
| `0x02`   | Merchant |
| `0x03`   | Inn      |
| `0x04`   | Gift     |
| `0x05`   | Fortune  |
| `0x06`   | Explorer |
| `0x07`   | Antiques |
| `0x08`   | Music    |
| `0x09`   | Casino   |
| `0x0a`   | Copy     |
