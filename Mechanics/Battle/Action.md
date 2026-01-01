The structure of the action section for both the player's party and the enemy's party is identical. The section is three bytes long and consists of:
* The target of the action
	* For single-target non-self actions, this is the combatant index
	* For all-target actions, this is either `0x80` for the player's party, or `0x40` for the enemy's party. This is a bit switch, which means that `0xc0` targets all combatants.
* The type of the action
* Item/spell ID
## Player's party
The current action of a member of the player's party is located:
* `+0x118` from the start of the party member's battle section
There are 5 actions a player's party member can do:

| ID  | Action  |
| --- | ------- |
| 0   | Examine |
| 1   | Attack  |
| 2   | Defend  |
| 4   | Ability |
| 5   | Item    |
ID 3 is supposed to be escape but this does not work for the player.
## Enemy's party
The current action of a member of the enemy's party is located
* `+0xf4` from the start of the enemy's battle section
There are 3 actions an enemy's party member can do:

| ID  | Action  |
| --- | ------- |
| 1   | Attack  |
| 2   | Defend  |
| 4   | Ability |
This section doesn't affect the targeting for some reason. See [[Target]].


