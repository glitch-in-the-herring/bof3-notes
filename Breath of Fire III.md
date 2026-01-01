<small>It's about time I put the notes for this game into a more organized format. </small>
Most of the notes here are only applicable to the US release of the game unless otherwise stated.

## Conventions
* All hexadecimal integers are big-endian.
* All hexadecimal integers are written in `monospace font`.
* If a hexadecimal integer appears inline, then it is marked with `0x`.
* If a hexadecimal integer appears next to a filename, then it is not marked. All file addresses are hexadecimal.
* All hexadecimal integers next to assembly code are their locations in the RAM and are always hexadecimal.
* All offsets are hexadecimal integers.
* A `+` sign in front of a hexadecimal integer indicates positive offset.
* A `-` sign in front of a hexadecimal integer indicates negative offset.
* When dealing with bit switches that span more than one byte, the bytes are not treated as little-endian integers, but rather as a byte string, thus they are presented in the order that they appear with the prefix `0x`.
* All binary integers are written as `monospace font` with a `0b` prefix.
* Differences in percentages are indicated using `pt`, thus an increase from 10% to 20% is an increase of 10pt, not 10%.
* The $\mathrm{rand}()$ function is an alias for the default random function that comes with the PSX's BIOS. This generates a random number between `0x0000` and `0x7fff`. This is rarely, if ever, used alone in practice. This function is normally called by jumping to `0x8016f384`
* The $\mathrm{random}(min, max)$ function is shorthand for the calculations done by the game using the value of $\mathrm{rand}()$ to obtain a random number between two integers `min` and `max`, inclusive.
* $R_{n}$ is used to denote the resistance number of the enemy. This means 200, 150, 100, etc., and not the percentage values.
* $R_n$ is always the target's resistance, because it makes no sense for it to be the caster's.
* Calculations are not simplified. If you see $\frac{100x}{100}$ in a formula, then that's how the game really does it. It calculates $100x$ then $\frac{100x}{100}$.
* Spoilers are not marked. If this is the first time you're playing the game, why are you reading this? Play it to the end before you open any other page.
* Conventions regarding directions can be found at [[Conventions]]