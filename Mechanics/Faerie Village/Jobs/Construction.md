The construction level of the village is stored at:
* in the RAM
* in the save file
## Clearing
The total active clearing power is the sum of the construction stat of faeries that are working the Clear job, It is stored at:
* `0x801455c5` in the RAM
## Building
The total active building power is the sum of the construction stat of faeries that are working the Build job, It is stored at:
* `0x801455c6` in the RAM
## Progressing
The overall progress of the construction jobs is stored as a bit switch at:
* `0x80144f46-80144f47` in the RAM
The number of battles that has elapsed is tracked at:
* `0x801455a8` in the RAM
The thresholds are located at:
* `0x80195fe0` in the RAM (permanent)
* `0x801ff590` in the RAM (temporary)
* `BIN/ETC/GAME.EMI: 00000fe0` in the game's files

| Position | Threshold Value | Type  |
| -------- | --------------- | ----- |
| 0        | 20              | Clear |
| 1        | 20              | Build |
| 2        | 20              | Build |
| 3        | 40              | Clear |
| 4        | 20              | Build |
| 5        | 20              | Build |
| 6        | 60              | Clear |
| 7        | 20              | Build |
| 8        | 20              | Build |
| 9        | 20              | Build |


Then it calculates the number of turns required to advance the job's progress. This is done by subtracting the active power from the threshold. If it is less than 5, then it is clipped to 5.
$$
b=\begin{cases}
T-C & T-C \geq 5\\
5 & T-C < 5
\end{cases}
$$
Then it gets the numeric progress of the construction. The numeric progress starts at 246 and goes up by one for every bit activated in the progress bit switch. The numeric progress also acts as a sort of index for the bits in the bit switch.

While the running numeric progress is less than 256, the game checks each corresponding bit in the bit switch. First, it gets the address of the byte by dividing the numeric progress by 8 (done by a bitshift right) and then adding it to a base address. Then, it gets the last hexadecimal digit of the numeric progress modulo 8, and right-shifts the current byte by that amount. It then checks if that bit is activated. If yes, then the numeric progress is incremented. If not, end loop. Repeat. 

After the loop, check how many faeries are actually working on the construction job. If nobody is working, then end the check. If there is at least one faerie working, then check if the current battle count is less than the threshold. If not, then set the next bit to active.

The battle counter stops incrementing when the next construction job does not match the active job. For example, if the next job is supposed to be clearing, but no faerie is working on it, then the counter does not increment. If both the clear and build jobs have at least one faerie working on them, then the job automatically alternates when the counter resets.

Each numeric progress value corresponds to an AREA file that is loaded when entering the village:

| Progress | AREA | No. of rooms |
| -------- | ---- | ------------ |
| 245      | 175  | 1            |
| 246      | 176  | 1            |
| 247      | 177  | 2            |
| 248      | 178  | 3            |
| 249      | 179  | 3            |
| 250      | 180  | 4            |
| 251      | 181  | 5            |
| 252      | 182  | 5            |
| 253      | 183  | 6            |
| 254      | 184  | 7            |
| 255      | 185  | 8            |

