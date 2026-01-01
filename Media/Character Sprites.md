Character sprites can be found in the `/BIN/PLCHAR` folder. These are supposed to be 8-bit images (i.e., eight bits/one byte = one pixel) , but in order to save space, the game stores six pixels together in a 32-bit integer, each pixel being five bits. The remaining two bits in the integer are ignored.
# Example
`73 be 24 00` has 32 bits. Written in binary, it becomes:
`01110011101111100010010000000000`
This is split up into six five bit sections as such:
`01 11001 11011 11100 01001 00000 00000`
With each five-bit section representing a pixel. The last two bits are discarded. The pixels are then added to the VRAM from right to left.