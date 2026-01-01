
$$
d = \begin{cases}
\iota - \left\lfloor\frac{65536\iota}{262144}\right\rfloor & \text{target is poisoned}\\
\iota & \text{otherwise}
\end{cases}
$$
$$
PWR_A' = PWR_A +\left\lfloor\frac{PWR_A\cdot \mathcal{F}}{2}\right\rfloor
$$
$$
\Delta PWR = \begin{cases}
PWR_A'  - \frac{1}{n}\sum_{k=1}^{n}DEF_{D_k}-DEF_{D_i} & PWR_A' - \frac{1}{n}\sum_{k=1}^{n}DEF_{D_k}-DEF_{D_i} \geq 0\\
0 & PWR_A' - \frac{1}{n}\sum_{k=1}^{n}DEF_{D_k}-DEF_{D_i} < 0
\end{cases}
$$
$$
I = \begin{cases}
-\left\lfloor\frac{\Delta PWR}{5}\right\rfloor & \Delta PWR < -4\\
0 & \Delta PWR \geq -4
\end{cases} 
$$
$$
\alpha = \begin{cases}
256\Delta PWR+\left\lfloor\frac{65536 L_A\mathrm{random}(2,3)}{256div[I]}\right\rfloor & \text{attacker is an enemy party member}\\
256\Delta PWR & \text{otherwise}
\end{cases}
$$
$$
\beta = \left\lfloor\frac{\alpha}{256}\right\rfloor + \mathrm{random}(0,1)
$$
$$
\gamma= 
256-\left\lfloor\frac{256\beta}{256000}\right\rfloor
$$
$$
\delta = \begin{cases}
\left\lfloor\frac{\gamma}{256}\right\rfloor & \left\lfloor\frac{\gamma}{256}\right\rfloor \geq 205\\
205 & \left\lfloor\frac{\gamma}{256}\right\rfloor < 205
\end{cases}
$$
$$
\epsilon = \left\lfloor\frac{256\beta\delta}{256}\right\rfloor
$$
$$
\zeta = 
\begin{cases}
\left\lfloor\frac{M\epsilon}{256}\right\rfloor & \left\lfloor\frac{M\epsilon}{256}\right\rfloor \&255  < 128\\
\left\lfloor\frac{M\epsilon}{256}\right\rfloor + 256 & \left\lfloor\frac{M\epsilon}{256}\right\rfloor \&255 \geq 128
\end{cases}
$$
$$
\eta = \left\lfloor\frac{256\zeta}{65536}\right\rfloor
$$
$$
\theta = \begin{cases}
\eta - \frac{G\eta}{100} & \text{target is defending}\\
\eta & \text{otherwise}
\end{cases}
$$
$$
\iota = \begin{cases}
\theta - \left\lfloor\frac{65536\theta}{262144}\right\rfloor & \text{defense formation}\\
\theta & \text{otherwise}
\end{cases}
$$

Where:
* $\mathcal{F}$ is the focus counter of the attacker
* $L_A$ is the attacker's level
* $div[i]$ is the array of the following values starting at $i=0$ :
	* 10, 11, 12, 13, 14, 15, 16, 18, 20
* $M$ is a multiplier from any of the following values:
	* 218, 230, 243, 256, 269, 282, 294, 307
* $G$ is a multiplier from any of the following values:
	* 50, 50, 50, 50, 60, 60, 60, 70