Faerie stats are located at:
* `0x801f2700` in the RAM
* In the following files:
```
BIN/ETC/COMMU00.EMI: 00004300
BIN/WORLD04/AREA175.EMI: 000cdb00
BIN/WORLD04/AREA176.EMI: 000c8b00
BIN/WORLD04/AREA177.EMI: 000c9300
BIN/WORLD04/AREA178.EMI: 000c9300
BIN/WORLD04/AREA179.EMI: 000c9300
BIN/WORLD04/AREA180.EMI: 000c9300
BIN/WORLD04/AREA181.EMI: 000c9300
BIN/WORLD04/AREA182.EMI: 000c9300
BIN/WORLD04/AREA183.EMI: 000c9b00
BIN/WORLD04/AREA184.EMI: 000c9b00
BIN/WORLD04/AREA185.EMI: 000c9b00
```
Faerie stats do not change over time. There are 60 faeries. Each entry is 9 bytes long and is structured as such:

| Position | Description                         | Value(s)               | Notes |
| -------- | ----------------------------------- | ---------------------- | ----- |
| 0-4      | Name                                | See the text guide     |       |
| 5        | Faerie's hunting power (PWR)        | 8-bit unsigned integer |       |
| 6        | Faerie's construction ability (CON) | 8-bit unsigned integer |       |
| 7        | Faerie's culture (CUL)              | 8-bit unsigned integer |       |
| 8        | Faerie's intelligence (INT)         | 8-bit unsigned integer |       |
