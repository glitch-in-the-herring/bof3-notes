The current active equipment for fishing is stored at:
* Fishing rod: `0x80145028` in the RAM
* Lure: `0x80145026` in the RAM
## General Table
The general table for fishing rods is located at:
* `0x801e2914` in the RAM
* In the following locations in the game's files:
```
BIN/WORLD00/AREA030.EMI: 0003dd14
BIN/WORLD02/AREA089.EMI: 0003dd14
BIN/WORLD03/AREA129.EMI: 0003dd14
```
There are six fishing rods. Each entry is 10 bytes long

| Position | Description                   | Value(s)                                                                                              | Note                                                                                                      |
| -------- | ----------------------------- | ----------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| 0        | Casting power speed           | 8-bit unsigned integer                                                                                |                                                                                                           |
| 1        | Casting power sweep direction | unsigned integer<br>0: Linear bidirectional<br>1: Linear unidirectional<br>2: Quadratic bidirectional |                                                                                                           |
| 2        | Maximum distance              | 8-bit unsigned integer                                                                                | Divide by 2 to get the value in meters                                                                    |
| 3        | Reeling cursor size           | 8-bit unsigned integer                                                                                |                                                                                                           |
| 4        | Reeling cursor return speed   | 8-bit signed integer                                                                                  | The speed at which the reeling cursor moves to the left side when the reel button is pressed              |
| 5        | Reeling cursor left speed     | 8-bit signed integer                                                                                  | The speed at which the reeling cursor moves to the left when the left button is pressed                   |
| 6        | Reeling cursor right speed    | 8-bit signed integer                                                                                  | The speed at which the reeling cursor moves to the right when the right button is pressed                 |
| 7        |                               |                                                                                                       |                                                                                                           |
| 8        | Snapping left tension         | 8-bit unsigned integer                                                                                | The tension value at which point the rod snaps when the reeling cursor is to the left of the fish cursor  |
| 9        | Snapping right tension        | 8-bit unsigned integer                                                                                | The tension value at which point the rod snaps when the reeling cursor is to the right of the fish cursor |
