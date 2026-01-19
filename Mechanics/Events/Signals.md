## `a0`

| Argument     | Value                  |
| ------------ | ---------------------- |
| 0: Signal ID | 8-bit unsigned integer |

The `a0` command is used to send a signal from an actor to other actors. 
## `a1`
| Argument     | Value                  |
| ------------ | ---------------------- |
| 0: Signal ID | 8-bit unsigned integer |

The `a1` command is used to receive a signal. When the actor receives the signal, it executes the commands that come after the receive command.
```
8015ba50 lbu    $v0, 0x0000(a0)
8015ba54 lbu    $v1, 0x0001(a0) ; load signal to anticipate
8015ba58 andi   $v0, 0x000c
8015ba5c srl    $v0, 0x02
8015ba60 lui    $at, 0x8014
8015ba64 addu   $at, $v0
8015ba68 lbu    $a1, 0x6864(at) ; load current counter
8015ba6c nop    
8015ba70 beq    $a1, $v1, 0x8015ba7c ; check if current counter is the signal
8015ba74 li     $v0, 0x0001; load 1 to advance the event script index by 1

; if the current signal is not the anticipated signal
8015ba78 li     $v0, -0x0x0001 ; subtract by 1 to not advance the event script index

8015ba7c jr     $ra 
```
The code can be found at `SLUS_004.22: 000c5a50`
## `a2`
The `a2` command increments the signal counter by 1.
```
8015ba84 lbu    $v1, 0x0000(a0)
8015ba88 nop    
8015ba8c andi   $v1, 0x000c
8015ba90 srl    $v1, 0x02
8015ba94 lui    $at, 0x8014
8015ba98 addu   $at, $v1
8015ba9c lbu    $v0, 0x6864(at) ; load current signal counter
8015baa0 nop    
8015baa4 addiu  $v0, 0x0001 ; add 1
8015baa8 lui    $at, 0x8014
8015baac addu   $at, $v1
8015bab0 sb     $v0, 0x6864(at) ; store new signal counter
8015bab4 jr     $ra
```
This code can be found at `SLUS_004.22: 000c5a84`