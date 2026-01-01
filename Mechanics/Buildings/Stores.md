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