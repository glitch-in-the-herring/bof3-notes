There are three subtypes of the exploration job:

| Byte   | Type    | Turns to update | Success Rate |
| ------ | ------- | --------------- | ------------ |
| `0x00` | Daytrip | 6               | 34.65%       |
| `0x01` | Nearby  | 12              | 44.55%       |
| `0x02` | Distant | 18              | 84.16%       |
## Turn requirement
The number of turns required for the game to update the exploration job is calculated by taking the byte of the trip type, adding one to it, and multiplying it by 6.
```
801ef838 lw     $a0, 0x502c(a0) ; load current battle count
801ef83c lui    $at, 0x8014
801ef840 addu   $at, $s3
801ef844 lw     $v0, 0x55cc(at) ; load last battle count
801ef848 lui    $at, 0x8014
801ef84c addu   $at, $fp
801ef850 lbu    $a1, 0x57a9(at) ; load trip type, let this be t
801ef854 subu   $a0, $v0
801ef858 addiu  $v1, $a1, 0x0001 ; t + 1
801ef85c sll    $v0, $v1, 0x01 ; 2(t+1)
801ef860 addu   $v0, $v1 ; 3(t+1)
801ef864 sll    $v0, 0x01 ; 6(t+1), this is the threshold for updating
801ef868 sltu   $a0, $v0 ; compare number of battles to the threshold
```
## Survival
If the number of battles is enough to update the job, then the game determines whether or not the faerie dies.
$$
r = 10(2t+1)-PWR_F\cdot (2t+1)
$$
$$
\begin{cases}
\mathrm{dead}&random(0,100) < r\\
\mathrm{alive}&random(0,100) \geq r\\
\end{cases}
$$
Where
* $t$ is the byte of the trip type
* $PWR_F$ is the hunting power of the faerie
## Success
If the faerie lives, then the game then determines whether or not the faerie's exploration was successful. The game rolls a `random(0,100)`, which is then compared to the threshold for the given trip type. The thresholds can be found at:
```
BIN/ETC/COMMU00.EMI: 00000804
BIN/WORLD04/AREA175.EMI: 000ca004
BIN/WORLD04/AREA176.EMI: 000c5004
BIN/WORLD04/AREA177.EMI: 000c5804
BIN/WORLD04/AREA178.EMI: 000c5804
BIN/WORLD04/AREA179.EMI: 000c5804
BIN/WORLD04/AREA180.EMI: 000c5804
BIN/WORLD04/AREA181.EMI: 000c5804
BIN/WORLD04/AREA182.EMI: 000c5804
BIN/WORLD04/AREA183.EMI: 000c6004
BIN/WORLD04/AREA184.EMI: 000c6004
BIN/WORLD04/AREA185.EMI: 000c6004
```
Each is an eight-bit unsigned integer matching the order of the trip types.
The status byte is assigned to the first free slot. There are three status bytes:

| Byte   | Status  |
| ------ | ------- |
| `0x00` | Waiting |
| `0x02` | Success |
| `0x03` | Failure |

## Reward
If the faerie successfully completes an exploration, the game will determine the reward when talking to the faerie. rolls $\mathrm{random}(0,100)$. It then checks the random number using the following tables, based on the trip type:
* Daytrip

| $\mathrm{random}(0,100)$ | Probability | Reward group |
| ------------------------ | ----------- | ------------ |
| 0-95                     | 95.05%      | 0            |
| 96-100                   | 5.05%       | 1            |

* Nearby

| $\mathrm{random}(0,100)$ | Probability | Reward group |
| ------------------------ | ----------- | ------------ |
| 0-80                     | 80.20%      | 0            |
| 81-100                   | 19.80%      | 1            |

* Distant

| $\mathrm{random}(0,100)$ | Probability | Reward group |
| ------------------------ | ----------- | ------------ |
| 0-55                     | 55.45%      | 0            |
| 56-85                    | 29.70%      | 1            |
| 86-100                   | 14.85%      | 2            |
The probability table can be found at:
* `0x801eec98` in the RAM
* In the following locations:
```
BIN/ETC/COMMU00.EMI: 00000898
BIN/WORLD04/AREA175.EMI: 000ca098
BIN/WORLD04/AREA176.EMI: 000c5098
BIN/WORLD04/AREA177.EMI: 000c5898
BIN/WORLD04/AREA178.EMI: 000c5898
BIN/WORLD04/AREA179.EMI: 000c5898
BIN/WORLD04/AREA180.EMI: 000c5898
BIN/WORLD04/AREA181.EMI: 000c5898
BIN/WORLD04/AREA182.EMI: 000c5898
BIN/WORLD04/AREA183.EMI: 000c6098
BIN/WORLD04/AREA184.EMI: 000c6098
BIN/WORLD04/AREA185.EMI: 000c6098
```
The game then rolls $\mathrm{random}(0,15)$ to decide which reward in the reward group to choose. 
* Reward group 1
	* Clay Vase
	* Clay Vase
	* Marbles
	* Marbles
	* Moldy Vase
	* Dirty Rags
	* Tea Cup
	* Beads
	* Life shard
	* Magic shard
	* Moxa
	* Wisdom Seed
	* Flame Shield
	* Breastplate
	* Mithril Helm
	* HiddenDagger
* Reward group 2
	* Dirty Rags
	* Tea Cup
	* Beads
	* Rare Book
	* Old Painting
	* Myria Icon
	* Ladon Icon
	* Power Food
	* Protein
	* Swallow Eye
	* Fish-head
	* AP Shells
	* Hawk's Ring
	* Artemis' Cap
	* Magma Armor
	* Ice Shield
* Reward group 3
	* Old Painting
	* Myria Icon
	* Ladon Icon
	* Litograph
	* Dragon Tear
	* Moon Tears
	* Ivory Charm
	* Spirit Ring
	* Wisdom Fruit
	* Force Armor
	* Lacquer Helm
	* Mind Shield
	* Deadly Blade
	* Ghostbuster
	* Beads
	* Rare Book

The rewards can be found at:
* `0x801f2618` in the RAM
* In the following files:
```
BIN/ETC/COMMU00.EMI: 00004218
BIN/WORLD04/AREA175.EMI: 000cda18
BIN/WORLD04/AREA176.EMI: 000c8a18
BIN/WORLD04/AREA177.EMI: 000c9218
BIN/WORLD04/AREA178.EMI: 000c9218
BIN/WORLD04/AREA179.EMI: 000c9218
BIN/WORLD04/AREA180.EMI: 000c9218
BIN/WORLD04/AREA181.EMI: 000c9218
BIN/WORLD04/AREA182.EMI: 000c9218
BIN/WORLD04/AREA183.EMI: 000c9a18
BIN/WORLD04/AREA184.EMI: 000c9a18
BIN/WORLD04/AREA185.EMI: 000c9a18
```
The rewards table follow the listing above. Each entry is two bytes long, the first being the item ID and the second being the item type.