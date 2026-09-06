As you progress through the game you'll meet masters who grant you new abilities as you level up
## Ordering

| ID     | Name        |
| ------ | ----------- |
| `0x00` | Bunyan      |
| `0x01` | Mygas       |
| `0x02` | Yggdrasil   |
| `0x03` | D'lonzo     |
| `0x04` | Fahl        |
| `0x05` | Durandal    |
| `0x06` | Giotto      |
| `0x07` | Hondara     |
| `0x08` | Emitai      |
| `0x09` | Deis        |
| `0x0a` | Hachio      |
| `0x0b` | Bais        |
| `0x0c` | Lang        |
| `0x0d` | Lee         |
| `0x0e` | Wynn        |
| `0x0f` | Ladon       |
| `0x10` | Meryleep    |
| `0xff` | (no master) |
## Spells
The spells that a master teaches can be found at:
* `0x801d4088` in the RAM
* `BIN/ETC/SISYOU.EMI: 00003c88` in the game's files
Each master has six spell entries. Each spell entry is two bytes in length and consists of:

| Position | Description     |
| -------- | --------------- |
| 1        | Level threshold |
| 2        | Spell ID        |
## Skill Granting
After the new skill is stored, the skill flag is then activated:
```
801d3dac lbu    $a1, 0x4089(at) ; load spell ID 
801d3db0 li     $v0, 0x0001
801d3db4 srl    $a0, $a1, 0x05 
801d3db8 sll    $a0, 0x02
801d3dbc addu   $a0, $s4 ; get byte position
801d3dc0 andi   $a1, 0x001f
801d3dc4 lw     $v1, 0x0000(a0) ; load old flag
801d3dc8 sllv   $v0, $a1 ; get bit position
801d3dcc or     $v1, $v0 ; activate bit
801d3dd0 j      0x801d3de8
801d3dd4 sw     $v1, 0x0000(a0) ; store new flag
```
The code can be found at `BIN/ETC/SISYOU.EMI: 000039ac`.
## Bonuses
The stat bonuses are located at:
* `0x801d4154` in the RAM
* `BIN/ETC/SISYOU.EMI: 00003d54` in the game's files
Each bonus entry consists of:

| Position | Stat |
| -------- | ---- |
| 1        | HP   |
| 2        | AP   |
| 3        | PWR  |
| 4        | DEF  |
| 5        | INT  |
| 6        | AGL  |
## Prerequisites
Some masters require you to meet certain requirements before you unlock them
### Bunyan
### Mygas
Mygas asks for all of your money, regardless of how much you have at hand, as long as it's not zero.
### Yggdrasil
### D'lonzo
D'lonzo requires you to carry 15 different weapons. 
```
80166470 lbu    $v0, 0x0000(a1) ; load weapon ID
80166474 nop    
80166478 beqz   $v0, 0x80166484
8016647c nop    

; If the weapon ID is not zero
80166480 addiu  $a2, 0x0001 ; increment weapon counter

; If the weapon ID is zero
80166484 addiu  $v1, 0x0001 ; increment loop counter
80166488 andi   $v0, $v1, 0x00ff
8016648c sltu   $v0, $a0
80166490 bnez   $v0, 0x80166470
80166494 addiu  $a1, 0x0001
...
801f38e8 sltiu  $v0, 0x000f ; check if weapon counter is greater than or equal to 15
```
### Hondara
Hondara requires you to learn Backhand from Durandal. He will check that flag when you talk to him:
```
801f2c18 lui    $v0, 0x8014 ; load base address for flag
801f2c1c lw     $v0, 0x4f94(v0) ; load flag
801f2c20 nop    
801f2c24 andi   $v0, 0x0020 ; check for Backhand
801f2c28 beqz   $v0, 0x801f2c40

; if flag bit is active
801f2c2c li     $v0, 0x0092

; if flag bit is inactive
801f2c40 li     $v0, 0x0093
```
This code can be found at `BIN/WORLD01/AREA074.EMI: 000ca018`.
### Meryleep
Meryleep requires you to have the Faerie Tiara to talk to her and the Flower Jewel to be able to apprentice under her. The Faerie Tiara check is done when the rock starts to hover above the pond.
```
801f2df4 move   $a0, $r0 ; set the inventory type ID to item
801f2df8 li     $a1, 0x0057 ; load the ID of the Faerie Tiara
801f2dfc jal    0x8016628c ; call the inventory checker function
...
801f2e04 bnez   $v0, 0x801f2e38
801f2e08 li     $v0, 0x0001
; if the quantity of Faerie Tiara is not zero
801f2e38 jal    0x8015c088 ; go here
801f2e3c nop      
```

```
801f2c18 move   $a0, $r0 ; set the inventory type ID to item
801f2c1c li     $a1, 0x0059 ; load the Flower Jewel's ID
801f2c20 jal    0x8016628c ; go to the inventory checker function
...
801f2c28 beqz   $v0, 0x801f2c54; check if the quantity is not zero
801f2c2c move   $a0, $r0
; If the quantity is not zero
801f2c30 li     $a1, 0x0059 ; load the Flower Jewel's ID
801f2c34 li     $a2, 0x0001 ; load the amount of Flower Jewels to take
801f2c38 jal    0x801665a0 ; go to the inventory taker function
801f2c3c move   $a3, $r0
...
```
Meryleep's requirements disregard the output of the item taker function. The first part can be found at `BIN/WORLD02/AREA091.EMI: 000aa1f4` and the second part at `BIN/WORLD02/AREA091.EMI: 000aa018`.