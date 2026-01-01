## Predetermined Dragon Forms
The abilities of predetermined dragon forms can be found at:
* `0x800b5008` in the RAM
*  In the following locations in the game's files:
```
BIN/BATTLE/BATTLE.EMI: 000a8808
BIN/BATTLE/BATTLE2.EMI: 000a8808
BIN/BOSS/BOSS001.EMI: 00066008
BIN/BOSS/BOSS002.EMI: 000a9808
BIN/BOSS/BOSS004.EMI: 00066008
BIN/BOSS/BOSS007.EMI: 000a8808
BIN/BOSS/BOSS008.EMI: 000a6808
BIN/BOSS/BOSS012.EMI: 000a9808
BIN/BOSS/BOSS013.EMI: 000a9808
BIN/BOSS/BOSS014.EMI: 000a8808
BIN/BOSS/BOSS015.EMI: 000a8808
BIN/BOSS/BOSS017.EMI: 000a9808
BIN/BOSS/BOSS018.EMI: 000a9808
BIN/BOSS/BOSS019.EMI: 000a9808
BIN/BOSS/BOSS020.EMI: 000a9808
BIN/BOSS/BOSS021.EMI: 000a9808
BIN/BOSS/BOSS022.EMI: 00066008
BIN/BOSS/BOSS023.EMI: 000a6808
BIN/BOSS/BOSS024.EMI: 000a9808
BIN/BOSS/BOSS025.EMI: 00066008
BIN/BOSS/BOSS027.EMI: 000a9808
BIN/BOSS/BOSS028.EMI: 000a9808
BIN/BOSS/BOSS029.EMI: 000a9808
BIN/BOSS/BOSS030.EMI: 000a9808
BIN/BOSS/BOSS031.EMI: 00066008
BIN/BOSS/BOSS032.EMI: 000a9808
BIN/BOSS/BOSS033.EMI: 000a8808
BIN/BOSS/BOSS034.EMI: 000a9808
BIN/BOSS/BOSS035.EMI: 000a9808
BIN/BOSS/BOSS036.EMI: 000a9808
BIN/BOSS/BOSS037.EMI: 000a9808
BIN/BOSS/BOSS038.EMI: 000a9808
BIN/BOSS/BOSS040.EMI: 000a9808
BIN/BOSS/BOSS042.EMI: 000a9808
BIN/BOSS/BOSS046.EMI: 000a9808
BIN/BOSS/BOSS047.EMI: 000a9808
BIN/BOSS/BOSS049.EMI: 000a9808
BIN/BOSS/BOSS050.EMI: 000a9808
BIN/BOSS/BOSS051.EMI: 000a9808
BIN/BOSS/BOSS052.EMI: 000a7008
BIN/BOSS/BOSS054.EMI: 000a9808
BIN/BOSS/BOSS055.EMI: 000ac808
```
All spells go to the "Attack" category. There are eight spell ID bytes for each predetermined dragon form. Adding optional genes where applicable does not change the ability set.

| Form                 | Abilities                                                                                              |
| -------------------- | ------------------------------------------------------------------------------------------------------ |
| (True) Kaiser        | KaiserBreath<br>Bonebreak<br>Howling                                                                   |
| Trygon               | FlameBreath<br>FrostBreath<br>ThundrBreath<br>DragonBreath<br>Snap                                     |
| Wildfire             | WhelpBreath<br>Charge                                                                                  |
| (Failed) Kaiser      | KaiserBreath<br>Bonebreak<br>Howling                                                                   |
| (Berserk) Kaiser     | KaiserBreath<br>Howling                                                                                |
| (Failed) Whelp       | WhelpBreath<br>Blind                                                                                   |
| Fusion*              |                                                                                                        |
| Tiamat<br>           | DoomBreath<br>ShadowBreath<br>VenomBreath                                                              |
| Myrmidon<br>         | Gambit<br>Aura<br>FlameStrike<br>ThundrStrike<br>FrostStrike<br>WindStrike<br>HolySTrike<br>AuraBreath |
| Mammoth              | Giant Growth<br>MeteorStrike                                                                           |
| Pygmy                | DragonBreath<br>Snap<br>Magma Breath                                                                   |
| Nina Hybrid          | Typhoon<br>Lightning<br>Inferno<br>Blizzard<br>Temptation                                              |
| Super Nina Hybrid    | Typhoon<br>Lightning<br>Inferno<br>Blizzard<br>Sirocco<br>Myollnir<br>Temptation                       |
| Peco Hybrid          | DreamBreath<br>VenomBreath<br>DragonBreath<br>Geo Breath                                               |
| Super Peco Hybrid    | DreamBreath<br>VenomBreath<br>DragonBreath<br>Gaea's Breath                                            |
| Unknown Hybrid       | Flame Breath<br>Flame Claw<br>Inferno                                                                  |
| Super Unknown Hybrid | Flame Breath<br>Flame Claw<br>Inferno                                                                  |
| Rei Hybrid           | Shadowwalk<br>DragonBreath<br>Tempest                                                                  |
| Super Rei Hybrid     | Shadowwalk<br>DragonBreath<br>Hurricane                                                                |
| Momo Hybrid          | Speed<br>Protect<br>Might<br>Restore<br>Remedy<br>Combustion                                           |
| Super Momo Hybrid    | Speed<br>Protect<br>Might<br>Restore<br>Remedy<br>Vitalize<br>Ragnarok<br>Combustion                   |
## Non-Predetermined Dragon Forms
Non-predetermined dragon forms have a base ability set and additional abilities based on their affinities. The base ability can be found at:
* `0x800b4ea4` in the RAM
* In the following locations in the game's files:
```
BIN/BATTLE/BATTLE.EMI: 000a86a4
BIN/BATTLE/BATTLE2.EMI: 000a86a4
BIN/BOSS/BOSS001.EMI: 00065ea4
BIN/BOSS/BOSS002.EMI: 000a96a4
BIN/BOSS/BOSS004.EMI: 00065ea4
BIN/BOSS/BOSS007.EMI: 000a86a4
BIN/BOSS/BOSS008.EMI: 000a66a4
BIN/BOSS/BOSS012.EMI: 000a96a4
BIN/BOSS/BOSS013.EMI: 000a96a4
BIN/BOSS/BOSS014.EMI: 000a86a4
BIN/BOSS/BOSS015.EMI: 000a86a4
BIN/BOSS/BOSS017.EMI: 000a96a4
BIN/BOSS/BOSS018.EMI: 000a96a4
BIN/BOSS/BOSS019.EMI: 000a96a4
BIN/BOSS/BOSS020.EMI: 000a96a4
BIN/BOSS/BOSS021.EMI: 000a96a4
BIN/BOSS/BOSS022.EMI: 00065ea4
BIN/BOSS/BOSS023.EMI: 000a66a4
BIN/BOSS/BOSS024.EMI: 000a96a4
BIN/BOSS/BOSS025.EMI: 00065ea4
BIN/BOSS/BOSS027.EMI: 000a96a4
BIN/BOSS/BOSS028.EMI: 000a96a4
BIN/BOSS/BOSS029.EMI: 000a96a4
BIN/BOSS/BOSS030.EMI: 000a96a4
BIN/BOSS/BOSS031.EMI: 00065ea4
BIN/BOSS/BOSS032.EMI: 000a96a4
BIN/BOSS/BOSS033.EMI: 000a86a4
BIN/BOSS/BOSS034.EMI: 000a96a4
BIN/BOSS/BOSS035.EMI: 000a96a4
BIN/BOSS/BOSS036.EMI: 000a96a4
BIN/BOSS/BOSS037.EMI: 000a96a4
BIN/BOSS/BOSS038.EMI: 000a96a4
BIN/BOSS/BOSS040.EMI: 000a96a4
BIN/BOSS/BOSS042.EMI: 000a96a4
BIN/BOSS/BOSS046.EMI: 000a96a4
BIN/BOSS/BOSS047.EMI: 000a96a4
BIN/BOSS/BOSS049.EMI: 000a96a4
BIN/BOSS/BOSS050.EMI: 000a96a4
BIN/BOSS/BOSS051.EMI: 000a96a4
BIN/BOSS/BOSS052.EMI: 000a6ea4
BIN/BOSS/BOSS054.EMI: 000a96a4
BIN/BOSS/BOSS055.EMI: 000ac6a4
```
Each dragon form has three base abilities.

| Form     | Abilities                       |
| -------- | ------------------------------- |
| Whelp    | Whelp Breath<br>Blind           |
| Dragon   | DragonBreath<br>Snap            |
| Warrior  | Gambit<br>Aura                  |
| Behemoth | MeteorStrike<br>Blitz<br>Charge |
After the base abilities have been added, the game then adds additional abilities based on the affinities. See [[Genes#Ability Sets]] for the list of abilities given by certain gene combinations. The last ability to be added to the ability list is the Restore Form ability.