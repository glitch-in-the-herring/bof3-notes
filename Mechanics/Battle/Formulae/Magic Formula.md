The magic formula is:

$$
d = \begin{cases}
\frac{1}{2}\delta & \text{target has barrier}\\
\delta & \text{otherwise}
\end{cases}
$$
$$
INT_A' = INT_A + \left\lfloor\frac{ INT_A\cdot \mathcal{M}}{2}\right\rfloor
$$
$$
\alpha = \left\lfloor\frac{100P(100 + INT_A')}{100}\right\rfloor
$$
$$
\beta = \begin{cases}
100 - \left\lfloor\frac{INT_D}{5}\right\rfloor & 100 - \left\lfloor\frac{INT_D}{5}\right\rfloor \geq 50 \\
50 & 100 - \left\lfloor\frac{INT_D}{5}\right\rfloor < 50
\end{cases}
$$
$$
\gamma = \left\lfloor\frac{\sum R_i\left\lfloor\frac{\alpha\beta}{100}\right\rfloor}{100}\right\rfloor
$$
$$
\delta = \left\lfloor\frac{M\gamma}{10000}\right\rfloor
$$
Where:
* $\mathcal{M}$ is the meditation counter of the attacker
* $P$ is the spell's power
* $M$ is a random multiplier from one of:
	* 85, 90, 95, 100, 105, 110, 115, 120
	* See [[Multipliers#Magic Formula|Multipliers]] for the location of these multipliers
* $R_i$ is the $i$-th resistance multiplier. This is summed up as $\sum R_i$, the total resistance multiplier. 
