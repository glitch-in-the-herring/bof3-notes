A door teleports the player from one place to another. It can be to another room in the same area, or it can be to a different area. While it is called a "door", it applies to anything that teleports the player, including stairs, end of paths, portals, etc.
A door consists of two parts: the door sill, and the door leaf. The door sill is the location where the door is placed, and is defined by the height map. This is what the game checks first when the player steps on a door tile. A door leaf is used to transport the player to another place. The door sill and door leaf should have the same location for the door to work.
To make things a bit simpler, the term "door" can be used to refer to both the door sill and the door leaf, if the distinction between the two is unnecessary.
## Door Sill
The door sill is the part of the map that indicates that there's supposed to be a  The door sill is indicated in the [[Height Map]] with a height value of `0xa_`, where:
* `0xa1` is the door sill of a level door
* `0xa2` is the door sill of a stairway
## Door Leaf
The

| Position | Description                       | Values                                                                            | Note |
| -------- | --------------------------------- | --------------------------------------------------------------------------------- | ---- |
| 0        | x coordinate position of the door | 8-bit unsigned integer                                                            |      |
| 1        | y coordinate position of the door | 8-bit unsigned integer                                                            |      |
| 2        | AREA file ID                      | 8-bit unsigned integer                                                            |      |
| 4-5      | Destination x coordinate          | 8-bit unsinged integer (integer part)<br>8-bit unsinged integer (fractional part) |      |
| 6-7      | Destination y coorditate          | 8-bit unsinged integer (integer part)<br>8-bit unsinged integer (fractional part) |      |
| 8        | Door x size                       | 8-bit unsigned integer                                                            |      |
| 9        | Door y size                       | 8-bit unsigned integer                                                            |      |


## Entering
The game first checks if the tile that the leading character is stepping on is a door sill:
```
801ba1a4 li     $v1, 0x00a0 
801ba1a8 bne    $a0, $v1, 0x801ba26c
801ba1ac li     $v0, 0x0010
801ba1b0 lbu    $v1, 0x0001(sp) ; load the current height map
801ba1b4 nop    
801ba1b8 andi   $v1, 0x00f0 ; get the first digit
801ba1bc bne    $v1, $a0, 0x801ba26c ; check if the first digit is 0xa
801ba1c0 nop    
801ba1c4 j      0x801ba26c
801ba1c8 li     $v0, 0x00a1 ; store the code for door sills
```
This code can be found at `BIN/ETC/GAME.EMI: 000251a4` in the game's files.
The game then checks the door leaves in the area and finds the one that matches the door sill.
