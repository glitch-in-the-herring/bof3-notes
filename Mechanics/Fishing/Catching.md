## Position
The position of the lure is located at:
* `0x80143ffc` in the RAM (x-axis)
* `0x80144000` in the RAM (y-axis)
* `0x80144004` in the RAM (z-axis/height)
The z-axis value decreases as the lure sinks, and vice versa.
## Catch
The ID of the fish currently being reeled in is located at `0x801e3208` in the RAM.
## Cursors
When reeling a fish, there are two cursors that are displayed in the HUD: the reeling cursor and the fish bar. To reel a fish in, the two cursors must be touching when the reel button is pressed.
The positions of the two cursors are determined by 8-bit signed integers. The center is 0, going left is going negative, and going right is going positive.
## Tension
Tension is stored in the pond data. The position of the reeling cursor and the fish cursor is checked every 3 frames. If the two are not in contact in that frame, then tension increases by 1. If they touch, then the tension is reset to 0.
The rod breaks if the tension is equal to the one of the snapping tensions of the rod and is at the correct position: left tension means the rod snaps when the reeling cursor is too far to the left, and right tension means the rod snaps when the reeling cursor is too far to the right.
## Reeling
Reeling speed is the same regardless of the rod being used. Every three frames, the y-axis position is increased by 4096 submeters if the fish and reeling cursors are touching.