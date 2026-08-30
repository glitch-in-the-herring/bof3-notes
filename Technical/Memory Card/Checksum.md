When you load a save file, the game calculates a checksum of that file to make sure that it has not been tampered with.
The game calculates the checksum by summing up the bytes in the save file starting from offset `+0x200` to `+0x12b0`, then extracting only the last two bytes. 
## Checking

```
801e5b04 lhu    $a3, 0x1a70(a3) ; load current hash in the save file
801e5b08 move   $a0, $r0
801e5b0c lui    $at, 0x800c
801e5b10 sh     $r0, 0x1a70(at) ; set the hash value to zero before the checksum calculation
; repeat 0x10b0 times
	801e5b14 lbu    $v0, 0x0000(v1) ; load current byte
	801e5b18 addiu  $a0, 0x0001 ; increment counter
	801e5b1c sb     $v0, 0x0000(a1) ; copy to this location
	801e5b20 lbu    $v0, 0x0000(v1) ; load current byte
	801e5b24 addiu  $v1, 0x0001 ; move pointer to the next byte
	801e5b28 addu   $a2, $v0 ; add current byte to the running sum
	801e5b2c andi   $v0, $a0, 0xffff ; clip the byte to the 16-bit limit
	801e5b30 sltiu  $v0, 0x10b0 ; loop 0x10b0 times
	801e5b34 bnez   $v0, 0x801e5b14
	801e5b38 addiu  $a1, 0x0001 ; increment copy location pointer
...
801e5b3c lui    $v0, 0x8014
801e5b40 lbu    $v0, 0x5025(v0)
801e5b44 lui    $at, 0x8014
801e5b48 sh     $v0, 0x6258(at)
801e5b4c andi   $v0, $a2, 0xffff ; extract only the last two bytes from the sum
801e5b50 beq    $v0, $a3, 0x801e5b68 ; check if the checksums are equal
```
This code can be found at
* `BIN/ETC/START.EMI: 0006cf04
* `BIN/ETC/STATUS.EMI: 00015704`
## Generating