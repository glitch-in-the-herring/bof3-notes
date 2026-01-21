
| Spell ID         | Targeting     | Power | AP  | Element |
| ---------------- | ------------- | ----- | --- | ------- |
| `0x44`<br>68<br> | `0xe`<br>Self | 0<br> | 0   | None    |
One of the most unique spells in Breath of Fire III, it "predicts" the outcome of the battle by looking at the stats of the combatants. The formula used to calculate this is given below:
$$
FS = LS + HPS + 8\|\{j|CHP_E[j] = 0\}\| + CS
$$
$$
LSI = \frac{1}{\|\{i|CHP_P[i] > 0\}\|}\sum_{i|CHP_P[i] > 0}L_P[i] - \frac{1}{\|\{j|CHP_E[j] > 0\}\|}\sum_{j|CHP_E[j] > 0}L_E[j]
$$
$$
LS = \begin{cases}
130 & LSI \geq 21\\
120 & 16 \leq LSI < 21\\
110 & 11 \leq LSI < 16\\
100 & 8 \leq LSI < 11\\
95 & 6 \leq LSI < 8\\
90 & 4 \leq LSI < 6\\
85 & 2 \leq LSI < 4\\
80 & 0 \leq LSI < 2\\
70 & -2 \leq LSI < 0\\
60 & -4 \leq LSI < -2\\
45 & -6 \leq LSI < -4
30 & -9 \leq LSI <-6\\
20 & -14 \leq LSI <-9\\
10 & -19 \leq LSI <-14\\
5 & LSI < -19
\end{cases} 
$$
$$
HPP_P[i] = \begin{cases}
-24 & CHP_P[i]/CMHP_P[i] = 0.00\\
-21 &0.00 < CHP_P[i]/CMHP_P[i] < 0.11\\
-18 &0.10 < CHP_P[i]/CMHP_P[i] < 0.21\\
-15 &0.20 < CHP_P[i]/CMHP_P[i] < 0.21\\
-12 &0.30 < CHP_P[i]/CMHP_P[i] < 0.21\\
-9 &0.40 < CHP_P[i]/CMHP_P[i] < 0.21\\
-6 &0.50 < CHP_P[i]/CMHP_P[i] < 0.21\\
-3 &0.60 < CHP_P[i]/CMHP_P[i] < 0.71\\
0 &CHP_P[i]/CMHP_P[i] > 0.70\\
\end{cases}
$$
$$
HPP_E[i] = \begin{cases}
24 & CHP_E[i]/CMHP_E[i] = 0.00\\
21 &0.00 < CHP_E[i]/MHP_E[i] < 0.11\\
18 &0.10 < CHP_E[i]/MHP_E[i] < 0.21\\
15 &0.20 < CHP_E[i]/MHP_E[i] < 0.21\\
12 &0.30 < CHP_E[i]/MHP_E[i] < 0.21\\
9 &0.40 < CHP_E[i]/MHP_E[i] < 0.21\\
6 &0.50 < CHP_E[i]/MHP_E[i] < 0.21\\
3 &0.60 < CHP_E[i]/MHP_E[i] < 0.71\\
0 &CHP_E[i]/CMHP_E[i] > 0.70\\
\end{cases}
$$
$$
HPS=\sum_{i=1}^{N_P}HPP_P[i]+\sum_{i=1}^{N_E}HPP_E[i]
$$
$$
CS = \begin{cases}
-12 & \|\{i|CHP_P[i] > 0\}\| - \|\{j|CHP_E[j] > 0\}\| = 2\\
-10 & \|\{i|CHP_P[i] > 0\}\| - \|\{j|CHP_E[j] > 0\}\| = 1\\
-8 & \|\{i|CHP_P[i] > 0\}\| - \|\{j|CHP_E[j] > 0\}\| = 0\\
-8 & \|\{i|CHP_P[i] > 0\}\| - \|\{j|CHP_E[j] > 0\}\| = -1\\
-6 & \|\{i|CHP_P[i] > 0\}\| - \|\{j|CHP_E[j] > 0\}\| = -2\\
-4 & \|\{i|CHP_P[i] > 0\}\| - \|\{j|CHP_E[j] > 0\}\| = -3\\
-2 & \|\{i|CHP_P[i] > 0\}\| - \|\{j|CHP_E[j] > 0\}\| = -4\\
0 & \|\{i|CHP_P[i] > 0\}\| - \|\{j|CHP_E[j] > 0\}\| = -5\\
\end{cases}
$$

Where:
* $CHP_P[i]$ is the current HP of the $i$-th party member
* $CHP_E[j]$ is the current HP of the $j$-th enemy
* $L_P[i]$ is the level of the $i$-th party member
* $L_E[j]$ is the level of the $j$-th party member
* $LSI$ is the level score index
* $LS$ is the level score
* $CMHP_P[i]$ is the current maximum HP of the $i$-th party member
* $MHP_E[j]$ is the maximum HP of the $j$-th enemy
* $HPP_P[i]$ is the HP points of the $i$-th party member
* $HPP_E[j]$ is the HP points of the $j$-th enemy
* $HPS$ is the HP score
* $CS$ is the count score
* $FS$ is the final score