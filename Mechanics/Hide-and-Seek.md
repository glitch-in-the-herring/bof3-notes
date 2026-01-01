There are two times where you get to play hide-and-seek. The first one is mandatory for the story progression and is done just after exiting the catacombs. The second one is optional but required if you want to unlock the masters Bais, Lang, Lee, and Wynn.
## Second game
The bit switch that is used to indicate that the player is taking part in the hide-and-seek game can be found at:
* `0x80144f36`, bit `0x04`, in the RAM
* `+0x85e`, bit `0x04` in the save file
The bit switches for the characters are:
* Bais:
	*  `0x80144f35`, bit `0x20` in the RAM
	* `+0x85d`, bit `0x20` in the save file
* Lang:
	* `0x80144f35`, bit `0x40` in the RAM
	* `+0x85d`, bit `0x40` in the save file
* Lee:
	*  `0x80144f36`, bit `0x01` in the RAM
	* `+0x85e`, bit `0x01` in the save file
* Wynn:
	*  `0x80144f36`, bit `0x02` in the RAM
	* `+0x85e`, bit `0x02` in the save file
Once all four are found, the bit flag:
*  `0x80144f35`, bit `0x80` in the RAM
* `+0x85d`, bit `0x80` in the save file
is toggled to 1.