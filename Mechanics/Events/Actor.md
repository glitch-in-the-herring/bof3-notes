## Base Table

| Position | Description           | Value(s)               | Note |
| -------- | --------------------- | ---------------------- | ---- |
| 7        | integer x position    | 8-bit unsigned integer |      |
| 8        | fractional x position | 8-bit unsigned integer |      |
| 9        | integer y position    | 8-bit unsigned integer |      |
| 10       | fractional y position | 8-bit unsigned integer |      |

## Scene Data

| Position | Description   | Value(s)                                                                            | Note |
| -------- | ------------- | ----------------------------------------------------------------------------------- | ---- |
| 39       | Color palette | 8-bit unsigned integer                                                              |      |
| 52-55    | x position    | 16-bit unsigned integer (fractional part)<br>16-bit unsigned integer (integer part) |      |
| 56-59    | y position    | 16-bit unsigned integer (fractional part)<br>16-bit unsigned integer (integer part) |      |
