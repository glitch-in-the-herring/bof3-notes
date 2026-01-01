During the Journey to Angel Tower arc, you get to train Beyd by fighting him.
## Data
When training Beyd he gets added to your party (temporarily) and his data is stored as the eighth party member, overwriting Whelp's data, at:
* `0x80144de4` in the RAM 
* in the save file
The data structure is the same as the other party members. See ... for info on that. This data sticks around after you fight Zig, effectively overwriting what was in Whelp's party data.
## Training
Normally you get 20 turns with Beyd.
### Max HP
Beyd's max HP increases based on the amount of damage dealt on him. The accumulated damage is stored at `0x801fe4e8` in the RAM. The max HP increase is calculated as 1/20th of the accumulated damage, rounded down.
### PWR
Beyd's base PWR increases based on the amount of damage he dealt. The accumulated damage is stored at `0x801fe4f0` in the RAM. The PWR increase is based on these ranges:

| Damage dealt | PWR increase |
| ------------ | ------------ |
| 0-50         | +2           |
| 50-80        | +4           |
| > 80         | +6           |
```
801d2630 sltiu  $v0, $a0, 0x0032 ; less than 50
801d2634 bnez   $v0, 0x801d2658
801d2638 li     $v0, 0x0002 ; set PWR increase to 2
801d263c addiu  $v0, $a0, -0x0032 ; -50 to the damage dealt
801d2640 sltiu  $v0, 0x001e ; damage dealt - 50 < 30, same as damage dealt < 80
801d2644 bnez   $v0, 0x801d2658
801d2648 li     $v0, 0x0004 ; set PWR increase to 4
801d264c sltiu  $v0, $a0, 0x0050 ; damage dealt < 80 
801d2650 bnez   $v0, 0x801d2660
801d2654 li     $v0, 0x0006 ; set PWR increase to 6
801d2658 lui    $at, 0x801e
801d265c sw     $v0, -0x7104(at) ; store PWR increase
```
The code can be found at `BIN/ETC/BATE.EMI: 00002230` in the game's files.
### DEF
Beyd's base DEF increases by the amount of blocked hits. One blocked hit equals one point of DEF. Any hit dealt when Beyd is defending counts as a blocked hit, including 0 damage hits and missed hits.
## Reward
When you visit Wharf after the fight with Zig, you will find two treasure chests. The one on the left contains a weapon, and the one on the right contains a chestplate. These are not the original equipment that you gave to Beyd. Instead, they are the equipment one ID above the ones you gave to Beyd. For example, if you gave Beyd a Scramasax, you get a Moon Sword in return.
### Weapon
```
801fc518 li     $a0, 0x0001 ; load item type (weapon)
801fc51c li     $a2, 0x0001 ; load item quantity
801fc520 lui    $s0, 0x8014 
801fc524 addiu  $s0, 0x4df2
801fc528 lbu    $a1, 0x0000(s0) ; load equipment given to Beyd
801fc52c move   $a3, $r0
801fc530 addiu  $a1, 0x0001 ; add 1 to the equpiment ID
801fc534 jal    0x801650b4 ; call inventory append function
801fc538 andi   $a1, 0x00ff
```
The code can be found at `BIN/SCENARIO/SCENA06.EMI: 00006118` in the game's files
### Armor
```
801fc5fc li     $a0, 0x0002 ; load item type (armor)
801fc600 li     $a2, 0x0001 ; load item amount
801fc604 lui    $s0, 0x8014
801fc608 addiu  $s0, 0x4df5
801fc60c lbu    $a1, 0x0000(s0) ; load equipment given to Beyd
801fc610 move   $a3, $r0
801fc614 addiu  $a1, 0x0001 ; add 1 to the equpiment ID
801fc618 jal    0x801650b4 ; call inventory append function
801fc61c andi   $a1, 0x00ff
801650b4 andi   $v1, $a1, 0x00ff
```
The code can be found at `BIN/SCENARIO/SCENA06.EMI: 000061fc` in the game's files