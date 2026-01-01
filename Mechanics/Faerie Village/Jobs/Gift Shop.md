The gift shop gives you an item after a certain number of battles.
The reward table can be found at:
* `0x801ff518` in the RAM
* In the following files:
```
BIN/ETC/COMMU00.EMI: 00000848
BIN/WORLD04/AREA175.EMI: 000ca048
BIN/WORLD04/AREA176.EMI: 000c5048
BIN/WORLD04/AREA177.EMI: 000c5848
BIN/WORLD04/AREA178.EMI: 000c5848
BIN/WORLD04/AREA179.EMI: 000c5848
BIN/WORLD04/AREA180.EMI: 000c5848
BIN/WORLD04/AREA181.EMI: 000c5848
BIN/WORLD04/AREA182.EMI: 000c5848
BIN/WORLD04/AREA183.EMI: 000c6048
BIN/WORLD04/AREA184.EMI: 000c6048
BIN/WORLD04/AREA185.EMI: 000c6048
```
Each entry is four bytes long and is structured as such:

| Position | Description                         | Values                  | Notes |
| -------- | ----------------------------------- | ----------------------- | ----- |
| 0-1      | Inclusive minimum number of battles | 16-bit unsigned integer |       |
| 2        | Item ID                             | 8-bit unsigned integer  |       |
| 3        | Item type                           | 8-bit unsigned integer  |       |
