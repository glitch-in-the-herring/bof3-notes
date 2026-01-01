The file table is located at
* `0x80182440` in the RAM
* `SLUS_004.22: 000ec440` in the game's files
Each entry is a 32-bit integer containing the start [[sector]] of each file. The files are ordered alphabetically. To get a file's size, multiply the difference between the file's start sector and the start sector of the next file by 2048.