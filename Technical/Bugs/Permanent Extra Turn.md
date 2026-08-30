## Description
The game does not clear the [[Turns#Extra Turns|extra turn]] flag for the third combatant in the player's party.
## Steps to Reproduce
### No gameplay effect (only visible in the RAM)
1. Make sure that there is only one party member whose AGL is above the extra turn threshold, that they are placed on the third position of your formation. Ideally you would use a [[Formations|formation]] that has no effect on your AGL. Make sure that you can decrease their AGL below the threshold during the battle, such as by putting equipment on them mid-battle or using a debuff on them.
2. Survive turn 1 fighting an enemy party whose extra turn threshold is lower than only the third position party member.
3. This party member should get a normal extra turn. Reduce this party member's AGL until it is no longer above the extra turn threshold.
4. Survive turn 2 and wait for the enemy's turn to finish.
5. Head to `0x80146238` in the RAM, which contains the third party member's extra turn flag. Notice that this is still on even though they shouldn't get an extra turn.
### Has gameplay effect (causes a permanent extra turn)
### Without the Chain Formation
1. Make sure that there are at least two party members whose AGL are above the extra turn threshold. Have one of them be placed on the third position of your formation. Ideally you would use a [[Formations|formation]] that has no effect on your AGL. Make sure that you can decrease the third position party member's AGL below the threshold during the battle, such as by putting equipment on them mid-battle or using a debuff on them.
2. Survive turn 1 fighting an enemy party whose extra turn threshold is lower than the aforementioned party members above.
3. On the first extra turn for these party members, reduce the third position party member's AGL until it is no longer above the extra turn threshold. Make sure there's still at least one other party member that can get an extra turn by having their AGL above the threshold.
4. Survive turn 2 and wait for the enemy's turn to finish.
5. Notice that even though the third position party member's AGL is no longer above the threshold, they still get an extra turn.
### With the Chain Formation
The bug as it was first reported to me by N.o.G on the Breath of Fire Discord server
1. Make sure that there is at least one party member whose AGL is above the extra turn threshold. Put them as the first position of the chain formation. Make sure that you can decrease the first position party member's AGL below the threshold during the battle by putting equipment on them. Make sure that you can also raise their AGL back by using the Speed buff.
2. Survive turn 1 fighting an enemy party whose extra turn threshold is lower than everyone's AGL (since they all have the same AGL at this point)
3. Everyone should have an extra turn. On this turn, have the first position party member put on some equipment so that their AGL decreases below the threshold. Everyone else's AGL should also decrease.
4. On the same extra turn, cast Speed on the first position party member. Make sure that this brings the first position party member's AGL up above the threshold. Everyone else's AGL should not change, because the Chain formation does not copy stat buffs.
5. Survive turn 2 and wait for the enemy's turn to finish.
6. First position party member should get an extra turn. Second position party member should not get an extra turn. Third position party member should get an extra turn.
## Cause
After an extra turn, the game has a function that clears the extra turn flags from the combatants:
```
801d4c50 lui    $a1, 0xffff ; load bits to clear the extra turn bit
801d4c54 ori    $a1, 0x7fff
...
801d4c70 lw     $v0, 0x5fb8(at) ; load flags
801d4c74 addiu  $a0, 0x0001
801d4c78 and    $v0, $a1 ; clear the extra turn bit
801d4c7c lui    $at, 0x8014
801d4c80 addu   $at, $v1
801d4c84 sw     $v0, 0x5fb8(at) ; store new flags
```
This code can be found at
```
BIN/BATTLE/BATTLE.EMI: 00047050
BIN/BATTLE/BATTLE2.EMI: 00047050
BIN/BOSS/BOSS001.EMI: 00004850
BIN/BOSS/BOSS002.EMI: 00048050
BIN/BOSS/BOSS004.EMI: 00004850
BIN/BOSS/BOSS007.EMI: 00047050
BIN/BOSS/BOSS008.EMI: 00045050
BIN/BOSS/BOSS012.EMI: 00048050
BIN/BOSS/BOSS013.EMI: 00048050
BIN/BOSS/BOSS014.EMI: 00047050
BIN/BOSS/BOSS015.EMI: 00047050
BIN/BOSS/BOSS017.EMI: 00048050
BIN/BOSS/BOSS018.EMI: 00048050
BIN/BOSS/BOSS019.EMI: 00048050
BIN/BOSS/BOSS020.EMI: 00048050
BIN/BOSS/BOSS021.EMI: 00048050
BIN/BOSS/BOSS022.EMI: 00004850
BIN/BOSS/BOSS023.EMI: 00045050
BIN/BOSS/BOSS024.EMI: 00048050
BIN/BOSS/BOSS025.EMI: 00004850
BIN/BOSS/BOSS027.EMI: 00048050
BIN/BOSS/BOSS028.EMI: 00048050
BIN/BOSS/BOSS029.EMI: 00048050
BIN/BOSS/BOSS030.EMI: 00048050
BIN/BOSS/BOSS031.EMI: 00004850
BIN/BOSS/BOSS032.EMI: 00048050
BIN/BOSS/BOSS033.EMI: 00047050
BIN/BOSS/BOSS034.EMI: 00048050
BIN/BOSS/BOSS035.EMI: 00048050
BIN/BOSS/BOSS036.EMI: 00048050
BIN/BOSS/BOSS037.EMI: 00048050
BIN/BOSS/BOSS038.EMI: 00048050
BIN/BOSS/BOSS040.EMI: 00048050
BIN/BOSS/BOSS042.EMI: 00048050
BIN/BOSS/BOSS046.EMI: 00048050
BIN/BOSS/BOSS047.EMI: 00048050
BIN/BOSS/BOSS049.EMI: 00048050
BIN/BOSS/BOSS050.EMI: 00048050
BIN/BOSS/BOSS051.EMI: 00048050
BIN/BOSS/BOSS052.EMI: 00045850
BIN/BOSS/BOSS054.EMI: 00048050
BIN/BOSS/BOSS055.EMI: 0004b050
```
However, the game only loops this code for the first two party members:
```
801d4c8c sltiu  $v0, 0x0002 
```
Hence, the third party member will never have their extra turn flag cleared if they already have it.
The game only checks the extra turn flag if there is a legitimate extra turn (i.e. another party member has an AGL that passes the threshold). If there are no legitimate extra turns, this flag is never checked and the party member in question will not get an extra turn.