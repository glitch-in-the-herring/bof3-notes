The merchant job type has three subtypes:
* Weapons (`0x00`): Sells weapons and armor
* Items (`0x01`): Sell items and accessories (mostly rings)
* Handyman (`0x02`): Sells items, accessories, and a weapon (ability subsubtype only)
Each has two subsubtypes: 
* Speed (`0x00`): Levels up faster
* Ability (`0x01`): Better items but takes longer to level up
The merchant uses INT to level up, with the level increase given by the formula below:
$$
\Delta L=\frac{m}{12 +6t-\sum_{i=1}^nCUL_i}
$$
Where:
* $m$ is the number of battles fought since last visiting the village
* $t$ is the subsubtype byte of the shop
* $CUL_i$ is the culture of the $i$-th faerie
* $n$ is the number of faeries working in the shop
The merchant's level cap is given as:
$$
L_{\max} = CUL_V+4
$$
Where $CUL_V$ is the culture level of the village.
The merchant room retains its level if all of the faeries in it are removed.