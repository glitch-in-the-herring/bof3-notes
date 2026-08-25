If the player successfully escapes, then the current battle is cancelled and no rewards are received. Enemies will always escape successfully. Any enemy that escapes cannot have their rewards be collected.

First, the game checks if the current escape attempt is the third or greater, in which case the escape will always succeed.
Otherwise, the game first calculates two values to determine the escape outcome, the player party AGL average and the truncated enemy party AGL average:
$$
\overline{AGL}_D = \frac{\sum_{i|\mathrm{alive}(i)} AGL_D[i]}{\|{i|\mathrm{alive}(i)}\|}
$$
$$
\overline{AGL}_{A_T} = \sum_{i=3}^7AGL_A[i]
$$
The enemy AGL average is called truncated because it only considers enemies from index 3 and onwards. This means that in a party of 3 or fewer enemies, their AGL average is zero.
The game then calculates the value $\Delta AGL$:
$$
\Delta AGL=\overline{AGL}_D - \overline{AGL}_{A_T}+32
$$
Then the game checks if $\Delta AGL$ is greater than or equal to zero. If it is, calculate $\alpha$ using this formula:
$$
\alpha = \left\lfloor\frac{\Delta AGL}{16}\right\rfloor
$$
If $\Delta AGL$ is negative, use this instead:
$$
\alpha = \left\lfloor\frac{\Delta AGL + 15}{16}\right\rfloor
$$If $\alpha$ is greater than 6, then let $\beta$ be 56. If $\alpha$ is less than 0, then let $\beta$ bet 28.
$$
\beta = \begin{cases}
56 & \alpha\geq6\\
28 & \alpha < 0
\end{cases}
$$
Anywhere in between, the game uses these values for $\beta$:

| $\alpha$ | $\beta$ |
| -------- | ------- |
| 0        | 32      |
| 1        | 36      |
| 2        | 40      |
| 3        | 44      |
| 4        | 48      |
| 5        | 52      |
This table can be found at:
* `0x800b44f0` in the RAM
* The following locations in the files:
```
BIN/BATTLE/BATTLE.EMI: 000a7cf0
BIN/BATTLE/BATTLE2.EMI: 000a7cf0
BIN/BOSS/BOSS001.EMI: 000654f0
BIN/BOSS/BOSS002.EMI: 000a8cf0
BIN/BOSS/BOSS004.EMI: 000654f0
BIN/BOSS/BOSS007.EMI: 000a7cf0
BIN/BOSS/BOSS008.EMI: 000a5cf0
BIN/BOSS/BOSS012.EMI: 000a8cf0
BIN/BOSS/BOSS013.EMI: 000a8cf0
BIN/BOSS/BOSS014.EMI: 000a7cf0
BIN/BOSS/BOSS015.EMI: 000a7cf0
BIN/BOSS/BOSS017.EMI: 000a8cf0
BIN/BOSS/BOSS018.EMI: 000a8cf0
BIN/BOSS/BOSS019.EMI: 000a8cf0
BIN/BOSS/BOSS020.EMI: 000a8cf0
BIN/BOSS/BOSS021.EMI: 000a8cf0
BIN/BOSS/BOSS022.EMI: 000654f0
BIN/BOSS/BOSS023.EMI: 000a5cf0
BIN/BOSS/BOSS024.EMI: 000a8cf0
BIN/BOSS/BOSS025.EMI: 000654f0
BIN/BOSS/BOSS027.EMI: 000a8cf0
BIN/BOSS/BOSS028.EMI: 000a8cf0
BIN/BOSS/BOSS029.EMI: 000a8cf0
BIN/BOSS/BOSS030.EMI: 000a8cf0
BIN/BOSS/BOSS031.EMI: 000654f0
BIN/BOSS/BOSS032.EMI: 000a8cf0
BIN/BOSS/BOSS033.EMI: 000a7cf0
BIN/BOSS/BOSS034.EMI: 000a8cf0
BIN/BOSS/BOSS035.EMI: 000a8cf0
BIN/BOSS/BOSS036.EMI: 000a8cf0
BIN/BOSS/BOSS037.EMI: 000a8cf0
BIN/BOSS/BOSS038.EMI: 000a8cf0
BIN/BOSS/BOSS040.EMI: 000a8cf0
BIN/BOSS/BOSS042.EMI: 000a8cf0
BIN/BOSS/BOSS046.EMI: 000a8cf0
BIN/BOSS/BOSS047.EMI: 000a8cf0
BIN/BOSS/BOSS049.EMI: 000a8cf0
BIN/BOSS/BOSS050.EMI: 000a8cf0
BIN/BOSS/BOSS051.EMI: 000a8cf0
BIN/BOSS/BOSS052.EMI: 000a64f0
BIN/BOSS/BOSS054.EMI: 000a8cf0
BIN/BOSS/BOSS055.EMI: 000abcf0
```
Check for the current escape attempt counter $\mathcal{C}$. If $\mathcal{C}$ is exactly 2 (the current attempt is the second escape attempt), then let $\gamma=\beta+8$. Otherwise, $\gamma=\beta$.
$$
\gamma = \begin{cases}
\beta+8 & \mathcal{C} = 2\\
\beta & \mathrm{otherwise}
\end{cases}
$$
Check every party member whose health is critical. Add eight times the number of critical party members $\mathcal{D}$ to gamma:
$$
\delta = \gamma + 8\mathcal{D}
$$
If $\delta > 64$, then cap it to 64.
$$
\epsilon = \begin{cases}
\delta & \delta < 65\\
64 & \delta > 64
\end{cases}
$$
Roll a random number from 0 to 63:
$$
r = \mathrm{random}(0,63)
$$
Then compare it with $\epsilon$ to determine the outcome of the escape:
$$
\begin{cases}
\mathrm{success} & r < \epsilon\\
\mathrm{fail} & r >= \epsilon
\end{cases}
$$
