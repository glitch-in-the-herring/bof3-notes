The data for all stores are stored in `/BIN/ETC/GAME.EMI`, regardless of location. Each store is defined by a store entry. Each entry is 23 bytes long and is structured as follows:

| Position                               | Description           | Value(s)                                                     | Notes                                                                       |
| -------------------------------------- | --------------------- | ------------------------------------------------------------ | --------------------------------------------------------------------------- |
| 0                                      | Number of items ($n$) | 8-bit unsigned integer                                       | There can be at most 11 items because of the size limitation of the section |
| 1 (and all odd positions up to $2n-1$) | Item type             | 0: Item<br>1: Weapon<br>2: Armor<br>3: Accessory<br>4: Vital |                                                                             |
| 2 (and all even positions up to $2n$)  | Item ID               | 8-bit unsigned integer                                       |                                                                             |
The store data is only loaded when the player hits the "Buy" button in the store menu. Upon entering the area that contains the store, the game loads the store index from the AREA file and stores it at `0x8014693c`. This index is the used to look up the store's data. The index is multiplied by 23 (the size of each store entry) and is added to the base address of the stores table. The base address is:
* `0x801ca28c` in the RAM
* `BIN/ETC/GAME.EMI: 0003528c` in the game's files
The address of the store entry is then stored in `0x8018e7cc`.
Discounts are calculated using this formula:
```
801daa04 lhu    $v0, -0x768c(at) ; load the item's original buying price
801daa08 j      0x801daa70
801daa0c nop    
801daa70 jr     $ra
801daa74 nop    
801e2fb0 lbu    $a1, 0x000b(s2) ; load the new price percentage
801e2fb4 jal    0x801d3654
801e2fb8 andi   $a0, $v0, 0xffff
801d3654 andi   $a1, 0xffff
801d3658 mult   $a0, $a1 ; multiply by the percentage
801d365c mflo   $v1, $lo
801d3660 lui    $v0, 0x51eb
801d3664 ori    $v0, 0x851f
801d3668 multu  $v1, $v0
801d366c mfhi   $a2, $hi
801d3670 srl    $v0, $a2, 0x05 ; multiply by the percentage
801d3674 bnez   $v0, 0x801d3680
801d3678 nop    
801d3680 jr     $ra
801d3684 nop    
```
This code can be found at `BIN/ETC/SHOP.EMI: 0000a604`.