## Description
In certain situations, a character may fail to be healed when using a healing spell in the world map
## Steps to Reproduce
1. Set the leading party member to anyone but Ryu
2. Go to the world map with this party ordering
3. Use a multi-target healing spell on your party
4. Notice that one of the party members, namely, the one who is leading, does not get healed
## Cause
The game for some reason copies your [[Field Party Data|field data]] to the [[Combatant Data (Player)|combatant data]] when you enter a world map. When copying, the data for the first player in the combatant data is always going to be Ryu, regardless of who is actually in the first position in the field ordering. That means if the second character in the field ordering is Ryu, then his data is going to be copied twice.