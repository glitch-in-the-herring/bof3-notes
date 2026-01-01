## General Table
The general table for fish is located at...

There are 23 entries. Each entry is 36 bytes long.

| Position | Description | Value(s) | Note |
| -------- | ----------- | -------- | ---- |

## Pond 
The array of fish in a fishing area is known as the pond. The pond starts at `0x80146888`. Each fish occupies 152 bytes in the pond.

| Position | Description          | Value(s)                                                                                    | Note |
| -------- | -------------------- | ------------------------------------------------------------------------------------------- | ---- |
| 6        | Fish ID              | 8-bit unsigned integer                                                                      |      |
| 10       | Fish cursor position | 8-bit signed integer                                                                        |      |
| 11       | Tension              | 8-bit unsigned integer                                                                      |      |
| 52-55    | x position           | 16-bit unsigned integer (fractional part)<br>16-bit unsigned integer (integer part)         |      |
| 56-59    | y position           | 16-bit unsigned integer (unused fractional part?)<br>16-bit unsigned integer (integer part) |      |
| 60-64    | z position/height    | 16-bit unsigned integer (unused fractional part?)<br>16-bit unsigned integer (integer part) |      |
| 142-143  | Stamina              | 16-bit unsigned integer                                                                     |      |
| 144      | Fish length          | 16-bit unsigned integer                                                                     |      |
## Populating
### Count
The fish count of each fishing spot is located at:
* `0x801e2df4` in the RAM
* In the following location in the game's files:
```
BIN/WORLD00/AREA030.EMI: 0003e1f4
BIN/WORLD02/AREA089.EMI: 0003e1f4
BIN/WORLD03/AREA129.EMI: 0003e1f4
```
Each fishing spot is allocated 23 bytes for each fish type. Each fish is allocated one byte for their count the pool. The order of the fish count corresponds to the index order of the fish.
### Location
The x coordinate of a fish is determined by using the formula $x=20-\mathrm{random}(0,15)$, which is then bit-shifted 16 bits to the left so that it's in the integer part of the coordinates.
The y coordinate of a fish is determined by using this formula:
$$
y=62-12D-\mathrm{random}(0,15)
$$
where $D$ is a random number from 0-3 referred to as the distance class.
The z coordinate of a fish is determined by using this formula:
$$z=-256H-32\mathrm{random}(0,7)$$
where $H$ is the height class of the fish.
### Length
Fish length is determined by the following algorithm:
1. Generate a random number $\mathrm{random}(0,255)$
2. Store this as the temporary length of the fish $l_t$
3. Load the current fish type's length threshold $L$
4. Check if $l_t \leq L$
5. If yes, then the final length $l$ is $l_t$
6. If not, then set $l_t$ to $l_t-\left\lfloor L/2\right\rfloor$ and repeat step 4.
## Stamina
Stamina is dependent on the fish's length:
$$
s = \left\lfloor\frac{S\left\lfloor\frac{10l}{L}\right\rfloor}{10}\right\rfloor
$$
where $S$ is the max stamina of the fish type.
## Record
The record data is located at
* `0x80144fe4` in the RAM
* `+0x90c` in the save file
Each fish is allocated one byte for their length. The order of the fish count corresponds to the index order of the fish.
The player's current fishing points are calculated using the following formula:
$$
P_i=\left\lfloor\frac{P_{i_\max}\left\lfloor\frac{10l}{l_{\max}}\right\rfloor}{10}\right\rfloor $$$$
P=\sum_{\mathrm{all}\,i} P_i
$$
Where:
* $P_i$ is the points from the $i$-th fish
* $P_{i_\max}$ is the maximum possible points of the $i$-th fish
* $l$ is the record length of the $i$-th fish
* $l_\max$ is the maximum possible length of the $i$-th fish 