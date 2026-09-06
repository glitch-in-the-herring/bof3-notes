Double Blow:

| Spell ID      | Targeting                              | Power | AP  | Element | Battle Spell Call |
| ------------- | -------------------------------------- | ----- | --- | ------- | ----------------- |
| `0x77`<br>119 | `0x6a`<br>Single<br>Always enemy party | 0     | 2   | None    | `0x49`            |

| Spell ID      | Targeting                              | Power | AP  | Element | Battle Spell Call |
| ------------- | -------------------------------------- | ----- | --- | ------- | ----------------- |
| `0x8d`<br>141 | `0x6a`<br>Single<br>Always enemy party | 0     | 5   | None    | `0x49`            |
Double Blow and Triple Blow both multiply the attacker's power by 0.8 before applying the [[Melee Formula]]:
```
8009fa90 lhu    $v1, 0x0000(a0) ; load attacker's PWR
8009fa94 ori    $a1, 0x851f
8009fa98 sll    $v0, $v1, 0x02 ; multiply attacker's PWR by 4
8009fa9c addu   $v0, $v1 ; multiply attacker's PWR by 5
8009faa0 sll    $v0, 0x04 ; multiply attacker's PWR by 80
8009faa4 mult   $v0, $a1 
8009faa8 mfhi   $a3, $hi
8009faac sra    $v0, $a3, 0x05 ; multiply attacker's PWR by 0.8
8009fab0 sh     $v0, 0x0000(a0) ; store new PWR
```
This code can be found at:
```
BIN/BATTLE/BATTLE.EMI: 00093290
BIN/BATTLE/BATTLE2.EMI: 00093290
BIN/BOSS/BOSS001.EMI: 00050a90
BIN/BOSS/BOSS002.EMI: 00094290
BIN/BOSS/BOSS004.EMI: 00050a90
BIN/BOSS/BOSS007.EMI: 00093290
BIN/BOSS/BOSS008.EMI: 00091290
BIN/BOSS/BOSS012.EMI: 00094290
BIN/BOSS/BOSS013.EMI: 00094290
BIN/BOSS/BOSS014.EMI: 00093290
BIN/BOSS/BOSS015.EMI: 00093290
BIN/BOSS/BOSS017.EMI: 00094290
BIN/BOSS/BOSS018.EMI: 00094290
BIN/BOSS/BOSS019.EMI: 00094290
BIN/BOSS/BOSS020.EMI: 00094290
BIN/BOSS/BOSS021.EMI: 00094290
BIN/BOSS/BOSS022.EMI: 00050a90
BIN/BOSS/BOSS023.EMI: 00091290
BIN/BOSS/BOSS024.EMI: 00094290
BIN/BOSS/BOSS025.EMI: 00050a90
BIN/BOSS/BOSS027.EMI: 00094290
BIN/BOSS/BOSS028.EMI: 00094290
BIN/BOSS/BOSS029.EMI: 00094290
BIN/BOSS/BOSS030.EMI: 00094290
BIN/BOSS/BOSS031.EMI: 00050a90
BIN/BOSS/BOSS032.EMI: 00094290
BIN/BOSS/BOSS033.EMI: 00093290
BIN/BOSS/BOSS034.EMI: 00094290
BIN/BOSS/BOSS035.EMI: 00094290
BIN/BOSS/BOSS036.EMI: 00094290
BIN/BOSS/BOSS037.EMI: 00094290
BIN/BOSS/BOSS038.EMI: 00094290
BIN/BOSS/BOSS040.EMI: 00094290
BIN/BOSS/BOSS042.EMI: 00094290
BIN/BOSS/BOSS046.EMI: 00094290
BIN/BOSS/BOSS047.EMI: 00094290
BIN/BOSS/BOSS049.EMI: 00094290
BIN/BOSS/BOSS050.EMI: 00094290
BIN/BOSS/BOSS051.EMI: 00094290
BIN/BOSS/BOSS052.EMI: 00091a90
BIN/BOSS/BOSS054.EMI: 00094290
BIN/BOSS/BOSS055.EMI: 00097290
```
## FAQ
* "Can you change how many hits they deal?" you can make them have less hits if you want.
* "How does the multi-hit mechanic work?" too long to explain even for a note that's supposed to be as comprehensive as possible
* "Please?" ok so basically the code for double, triple, and multistrike are stored in MAGIC018.EMI. You may recognize spell ID 18 as Giant Growth. The game has a counter that goes up when performing the attacks. Each number of the counter corresponds with a function to be executed. The functions attached to counter values 0, 3, and 6 deal the attack to the target. There is a part of the game that keeps track whether or not the counter has exceeded a certain command, but you can't add any more functions after the eight counter. That's the most distilled explanation that I can give.