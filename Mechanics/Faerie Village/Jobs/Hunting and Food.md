To survive, the faerie village needs to have food. Food is obtained by sending faeries out to hunt.
The amount of food currently available in the village is located at:
* `0x801455c2` in the RAM
* `+0xeeb` in the save file
The number of food that is in the faerie village with a living population of $N$ and a hunting team of size $N_h\leq N$ after you have fought $m$ battles is given by:
$$
F = F_0 + \left\lfloor\frac{m}{5}\right\rfloor\Delta F
$$
$$
\Delta F = I-O
$$
$$
I = \sum_{i=1}^{N_h} (PWR_k + 3)
$$
$$
O = 2N
$$
Where $PWR_k$ is the power of the $k$-th faerie.