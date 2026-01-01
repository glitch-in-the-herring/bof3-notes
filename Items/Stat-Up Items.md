These items increase the target's stats permanently and can only be used in the field normally.
## Life Shard
| ID           | Flags | Price |
| ------------ | ----- | ----- |
| `0x19`<br>25 |       |       |
Life Shard increases the target's maximum HP by 1 permanently:
```
801e8400 addiu  $a0, $s0, 0x003c ; set the stat to HP
801e8404 jal    0x8016546c ; go to stat change function
801e8408 li     $a1, 0x0001 ; set change to 1
```
The code can be found at:
```
BIN/ETC/START.EMI: 0006f800
BIN/ETC/STATUS.EMI: 00018000
```
## Magic Shard
| ID           | Flags | Price |
| ------------ | ----- | ----- |
| `0x1a`<br>26 |       |       |
Magic Shard increases the target's maximum AP by 1 permanently:
```
801e849c addiu  $a0, $s0, 0x003e ; set the stat to AP
801e84a0 jal    0x8016546c ; go to stat change function
801e84a4 li     $a1, 0x0001 ; set change to 1
```
The code can be found at:
```
BIN/ETC/START.EMI: 0006f89c
BIN/ETC/STATUS.EMI: 0001809c
```
## Power Food

| ID           | Flags | Price |
| ------------ | ----- | ----- |
| `0x1b`<br>27 |       |       |
Power food increases the target's PWR stat by 1 permanently:
```
801e8544 addiu  $a0, $s0, 0x0020 ; set the stat to PWR
801e8548 li     $a1, 0x0001 ; load PWR increase
801e854c jal    0x801654f4 ; go to stat increase function
```
The code can be found at:
```
BIN/ETC/START.EMI: 0006f944
BIN/ETC/STATUS.EMI: 00018144
```
## Protein
| ID           | Flags | Price |
| ------------ | ----- | ----- |
| `0x1c`<br>28 |       |       |
Protein increases the target's DEF stat by 1 permanently:
```
801e85e0 addiu  $a0, $s0, 0x0022 ; set the stat to DEF
801e85e4 li     $a1, 0x0001 ; load DEF increase
801e85e8 jal    0x801654f4 ; go to stat increase function
```
The code can be found at:
```
BIN/ETC/START.EMI: 0006f9e0
BIN/ETC/STATUS.EMI: 000181e0
```
## Swallow Eye
| ID           | Flags | Price |
| ------------ | ----- | ----- |
| `0x1d`<br>29 |       |       |
Swallow Eye increases the target's SPD by 1 permanently:
```
801e867c addiu  $a0, $s0, 0x0024 ; set the stat to SPD
801e8680 li     $a1, 0x0001 ; load SPD increase
801e8684 jal    0x801654f4 ; go to stat increase function
```

The code can be found at:
```
BIN/ETC/START.EMI: 0006fa7c
BIN/ETC/STATUS.EMI: 0001827c
```
## Fish-Head
| ID           | Flags | Price |
| ------------ | ----- | ----- |
| `0x1e`<br>30 |       |       |
Fish-Head increases the target's INT by 1 permanently:
```
801e8718 addiu  $a0, $s0, 0x0026 ; set the stat to INT
801e871c li     $a1, 0x0001 ; load INT increase
801e8720 jal    0x801654f4 ; go to stat increase function
```

The code can be found at:
```
BIN/ETC/START.EMI: 0006fb18
BIN/ETC/STATUS.EMI: 00018318
```
## Moxa
Moxa increases the target's Willpower by 1 permanently:
```
801e87a8 addiu  $a0, $s0, 0x004a ; set the stat to Willpower
801e87ac jal    0x801654b0 ; go to moxa increase function
801e87b0 li     $a1, 0x0001 ; 
```
The code can be found at:
```
BIN/ETC/START.EMI: 0006fba8
BIN/ETC/STATUS.EMI: 000183a8
```