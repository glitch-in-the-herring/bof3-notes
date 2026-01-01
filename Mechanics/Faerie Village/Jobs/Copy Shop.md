The copy shop allows the player to copy certain items, though it has a chance of failing. It can either fail normally (the faerie gives back your item) or spectacularly (whatever item you copied becomes a useless rice ball).
When you give an item to the copy shop, the item's quantity in the inventory is reduced by one. The item is also removed from the inventory item ID table if necessary. In the shop's data section, the game inserts the item's ID to the item ID slot and sets the copy status to `0x10`, indicating the item is not ready. 
The item's ID is stored in the first free byte of the [[Faerie Job Data]], while the status is stored in the second free byte. The status bytes are:

| Status | Description                                                   |
| ------ | ------------------------------------------------------------- |
| `0x20` | Success<br>Two of the copied item is returned                 |
| `0x30` | Normal Failure<br>Item is returned                            |
| `0x40` | Spectacular Failure<br>Sets your copied item to the rice ball |
The game checks for the item's price when copying, and has a table of price categories with relevant values for calculating the success rate and number of battles required for the copy shop to update. This can be found at:
* `0x801f2530` in the RAM
* In the following files:
```
BIN/ETC/COMMU00.EMI: 00004130
BIN/WORLD04/AREA175.EMI: 000cd930
BIN/WORLD04/AREA176.EMI: 000c8930
BIN/WORLD04/AREA177.EMI: 000c9130
BIN/WORLD04/AREA178.EMI: 000c9130
BIN/WORLD04/AREA179.EMI: 000c9130
BIN/WORLD04/AREA180.EMI: 000c9130
BIN/WORLD04/AREA181.EMI: 000c9130
BIN/WORLD04/AREA182.EMI: 000c9130
BIN/WORLD04/AREA183.EMI: 000c9930
BIN/WORLD04/AREA184.EMI: 000c9930
BIN/WORLD04/AREA185.EMI: 000c9930
```
Each entry is six bytes long and is structured like so:

| Position | Description                          | Values                  | Note |
| -------- | ------------------------------------ | ----------------------- | ---- |
| 0-1      | Max price for this category          | 16-bit unsigned integer |      |
| 2-3      | Number of battles required to update | 16-bit unsigned integer |      |
| 4-5      | Multiplier                           | 16-bit unsigned integer |      |
By default these values are:

| Price range            | Number of battles | Multiplier ($M$) |
| ---------------------- | ----------------- | ---------------- |
| $0<P\leq100$           | 10                | 60               |
| $100 < P \leq 300$     | 12                | 50               |
| $300 <P \leq 500$      | 14                | 40               |
| $500 < P \leq 1000$    | 16                | 35               |
| $1000 < P \leq 3000$   | 18                | 30               |
| $3000 <P \leq 10000$   | 20                | 25               |
| $10000 < P \leq 30000$ | 22                | 20               |
| $30000< P \leq 65536$  | 24                | 10               |
Where $P$ is the buy price of the item.

The game uses the following formula to compute the success of the copy shop:
$$
r = M + \left\lfloor\frac{M\cdot INT_F}{20}\right\rfloor
$$


$$
\begin{cases}
\text{Success} & \mathrm{random}(0,100)_0 < r\\
\text{Normal Failure}&\mathrm{random}(0,100)_0 \geq r \wedge\mathrm{random}(0,100)_1\geq 30 - 2INT_F\\
\text{Spectacular Failure}&\mathrm{random}(0,100)_0 \geq r\wedge\mathrm{random}(0,100)_1< 30 - 2INT_F
\end{cases}
$$
Where $INT_F$ is the faerie's intelligence.

The code can be found in the following files:
```
BIN/ETC/COMMU00.EMI: 00001748
BIN/WORLD04/AREA175.EMI: 000caf48
BIN/WORLD04/AREA176.EMI: 000c5f48
BIN/WORLD04/AREA177.EMI: 000c6748
BIN/WORLD04/AREA178.EMI: 000c6748
BIN/WORLD04/AREA179.EMI: 000c6748
BIN/WORLD04/AREA180.EMI: 000c6748
BIN/WORLD04/AREA181.EMI: 000c6748
BIN/WORLD04/AREA182.EMI: 000c6748
BIN/WORLD04/AREA183.EMI: 000c6f48
BIN/WORLD04/AREA184.EMI: 000c6f48
BIN/WORLD04/AREA185.EMI: 000c6f48
```

```
801efb48 lhu    $a0, -0x768c(at) ; load the price of the item
801efb4c lui    $at, 0x801d
801efb50 addu   $at, $v0
801efb54 lbu    $a2, -0x7690(at) ; load the item's flags
801efb58 j      0x801efc18
801efb5c move   $v1, $r0 ; set counter to 0
801efc18 andi   $a1, $a0, 0xffff
801efc1c move   $a0, $r0 ; set offset to 0
801efc20 lui    $at, 0x801f
801efc24 addu   $at, $a0 ; add offset to base address
801efc28 lhu    $v0, 0x2530(at) ; load price threshold 
801efc2c nop    
801efc30 sltu   $v0, $a1 ; compare price threshold
801efc34 beqz   $v0, 0x801efc50
801efc38 sll    $v0, $v1, 0x01

; if the item's price is still above the threshold continue loop
801efc3c addiu  $v1, 0x0001 ; add 1 to the counter
801efc40 slti   $v0, $v1, 0x0008 ; counter < 8
801efc44 bnez   $v0, 0x801efc20
801efc48 addiu  $a0, 0x0006 ; add 6 to the offset

; if the item's price is below the threshold
801efc50 addu   $v0, $v1 ; counter * 3
801efc54 sll    $a1, $v0, 0x01 ; counter * 12 = multiplier offset
801efc58 lui    $v0, 0x8014
801efc5c lw     $v0, 0x502c(v0) ; load current number of battles
801efc60 lui    $at, 0x8014
801efc64 addu   $at, $s1
801efc68 lw     $v1, 0x55cc(at) ; load number of battles last time visiting the village
801efc6c lui    $at, 0x801f
801efc70 addu   $at, $a1
801efc74 lhu    $a0, 0x2532(at) ; load number of battles needed to update the copy shop
801efc78 subu   $v0, $v1 ; get the number of battles fought since last visting the village
801efc7c sltu   $v0, $a0
801efc80 bnez   $v0, 0x801efe5c
801efc84 nop    

; if enough battles were fought
801efc88 lui    $at, 0x8014
801efc8c addu   $at, $s1
801efc90 lbu    $v0, 0x55cb(at) ; load the current status
801efc94 nop    
801efc98 andi   $v1, $v0, 0x000f
801efc9c andi   $v0, $a2, 0x0008 ; get the unsellable bit
801efca0 lui    $at, 0x8014
801efca4 addu   $at, $s1
801efca8 sb     $v1, 0x55cb(at)
801efcac beqz   $v0, 0x801efcc8
801efcb0 ori    $v0, $v1, 0x0030

; if the item is sellable
801efcc8 lui    $at, 0x801f
801efccc addu   $at, $a1 ; offset + base address
801efcd0 lhu    $a0, 0x2534(at) ; load multiplier for the item price class, let this be M
801efcd4 lbu    $v0, 0x0000(s2) ; load the faerie's int
801efcd8 nop    
801efcdc mult   $a0, $v0 ; M * int
801efce0 mflo   $v0, $lo
801efce4 lui    $v1, 0x6666
801efce8 ori    $v1, 0x6667
801efcec mult   $v0, $v1 ; M * int * 0.4
801efcf0 sra    $v0, 0x1f
801efcf4 mfhi   $a3, $hi
801efcf8 sra    $v1, $a3, 0x03 ; M * int * 1/20
801efcfc subu   $v1, $v0
801efd00 addu   $a0, $v1 ; M * int * 1/20 + M, let this be r
801efd04 move   $s0, $a0
801efd08 sll    $a0, 0x10
801efd0c sra    $v0, $a0, 0x10
801efd10 bltz   $v0, 0x801efd28
801efd14 slti   $v0, 0x0065
801efd18 bnez   $v0, 0x801efd2c
801efd1c move   $v1, $s0

; if r is less than or equal to 100
801efd2c jal    0x8017e3d4 
801efd30 move   $s0, $v1
8017e3d4 li     $t2, 0x00a0
8017e3d8 jr     $t2 ; get random number
8017e3dc li     $t1, 0x002f
...
801efd34 andi   $v1, $v0, 0x007f ; random number from 0-127
801efd38 slti   $v0, $v1, 0x0065

801efd3c bnez   $v0, 0x801efd48
801efd40 move   $a0, $v1

; if the random number is greater than 100
801efd44 addiu  $a0, $v1, -0x001c ; subtract 28 from the random number

; if the random number is less than or equal to 100
801efd48 sll    $v1, $s0, 0x10
801efd4c sra    $v1, 0x10
801efd50 sll    $v0, $a0, 0x10
801efd54 sra    $v0, 0x10
801efd58 slt    $v0, $v1 
801efd5c beqz   $v0, 0x801efd8c
801efd60 li     $v1, 0x001e

; if the random number is less than or equal to the threshold
801efd64 lui    $at, 0x8014
801efd68 addu   $at, $s1
801efd6c lbu    $v0, 0x55cb(at)
801efd70 nop    
801efd74 ori    $v0, 0x0020 ; set the status to success
801efd78 lui    $at, 0x8014
801efd7c addu   $at, $s1
801efd80 sb     $v0, 0x55cb(at) ; store status

; if the random number is greater than threshold
801efd60 li     $v1, 0x001e ;
801efd8c lbu    $v0, 0x0000(s2) ; read faerie's int again
801efd90 nop    
801efd94 sll    $v0, 0x01 ; int * 2
801efd98 jal    0x8017e3d4 ; generate random number
801efd9c subu   $s0, $v1, $v0 ; 30 - int*2
8017e3d4 li     $t2, 0x00a0
8017e3d8 jr     $t2
8017e3dc li     $t1, 0x002f
...
801efda0 andi   $v1, $v0, 0x007f ; random number from 0-127
801efda4 slti   $v0, $v1, 0x0065
801efda8 bnez   $v0, 0x801efdb4
801efdac move   $a0, $v1

; if the random number is greater than 100
801efdb0 addiu  $a0, $v1, -0x001c ; subtract 28 from the random number

; if the random number is less than or equal to 100
801efdb4 sll    $v0, $a0, 0x10
801efdb8 sra    $v0, 0x10
801efdbc slt    $v0, $s0 
801efdc0 bnez   $v0, 0x801efdf0

; if the random number is less than 30 - int*2
801efdc4 li     $v0, 0x0040 ; set the status to spectacular failure
801efdf0 lui    $at, 0x8014
801efdf4 addu   $at, $s1
801efdf8 sb     $v0, 0x55cb(at) ; store status
801efdfc li     $v0, 0x0037 ; item ID of rice ball
801efe00 lui    $at, 0x8014
801efe04 addu   $at, $s1
801efe08 sb     $v0, 0x55ca(at) ; store item

; if the random number is greater than or equal to 30 - int*2
801efdc8 lui    $at, 0x8014
801efdcc addu   $at, $s1
801efdd0 lbu    $v0, 0x55cb(at)
801efdd4 nop    
801efdd8 ori    $v0, 0x0030 ; set the status to normal failure
801efddc lui    $at, 0x8014
801efde0 addu   $at, $s1
801efde4 sb     $v0, 0x55cb(at) ; store status
```
Upon success, the game adds two to the copied item's quantity. This increment is not stored in the assembly. Instead, it is stored in the data, which can be found at:
* `0x801f26dc` in the RAM
* In the following locations in the files:
```
BIN/ETC/COMMU00.EMI: 000042dc
BIN/WORLD04/AREA175.EMI: 000cdadc
BIN/WORLD04/AREA176.EMI: 000c8adc
BIN/WORLD04/AREA177.EMI: 000c92dc
BIN/WORLD04/AREA178.EMI: 000c92dc
BIN/WORLD04/AREA179.EMI: 000c92dc
BIN/WORLD04/AREA180.EMI: 000c92dc
BIN/WORLD04/AREA181.EMI: 000c92dc
BIN/WORLD04/AREA182.EMI: 000c92dc
BIN/WORLD04/AREA183.EMI: 000c9adc
BIN/WORLD04/AREA184.EMI: 000c9adc
BIN/WORLD04/AREA185.EMI: 000c9adc
```