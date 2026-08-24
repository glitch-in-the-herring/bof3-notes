Background music is stored in `/BIN/BGM/`. A single .EMI file can store multiple BGM.
## Music loading
The game uses the following algorithm to load music:
1. The game first loads the AREA ID of the target area
2. The game then compares this ID with the known IDs of world map AREAs. This list can be found at:
	* `0x801c8384` in the RAM
	* `BIN/ETC/GAME.EMI: 00033384` in the game's files
	There are 11 IDs, each two bytes long. All of the IDs are IDs of world map AREAs
3. If the AREA ID matches a world map AREA, go to 4. If not, go to ...
4. 