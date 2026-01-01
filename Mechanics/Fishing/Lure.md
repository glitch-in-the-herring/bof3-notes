## General Table
The general table for the lures can be found at:
* `0x801e2950` in the RAM
* In the following locations in the game's files:
```
BIN/WORLD00/AREA030.EMI: 0003dd50
BIN/WORLD02/AREA089.EMI: 0003dd50
BIN/WORLD03/AREA129.EMI: 0003dd50
```
Each entry is 20 bytes long and is structured as such:

| Position | Description         | Value(s)       | Note                                    |
| -------- | ------------------- | -------------- | --------------------------------------- |
| 1-3      | Idle float rate     | 16-bit integer | Negative number causes the lure to sink |
| 4-7      | Reeling float rate  | 16-bit integer | Negative number causes the lure to sink |
| 8-11     | Sideways float rate | 16-bit integer | Negative number causes the lure to sink |
|          |                     |                |                                         |
