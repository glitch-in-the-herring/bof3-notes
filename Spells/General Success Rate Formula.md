Spells that have a chance of failing use this formula to determine their success:
$$
\begin{cases}
\mathrm{success} & \mathrm{random}(0,99) < r\\
\mathrm{fail} & \mathrm{random}(0,99) \geq r\\
\end{cases}
$$

$$
r = \left\lfloor\frac{\alpha\beta R}{10000}\right\rfloor
$$
$$
\alpha= \begin{cases}
\left\lfloor\frac{INT_{A}}{5}\right\rfloor + 50 & \left\lfloor\frac{INT_{A}}{5}\right\rfloor + 50 < 100\\
100 & \left\lfloor\frac{INT_{A}}{5}\right\rfloor + 50 \geq 100
\end{cases}
$$
$$
\beta = \begin{cases}
125 - \left\lfloor\frac{INT_{D}}{5}\right\rfloor  & 125 - \left\lfloor\frac{INT_{D}}{5}\right\rfloor \geq 50\\
50 & 125 - \left\lfloor\frac{INT_{D}}{5}\right\rfloor < 50
\end{cases}
$$