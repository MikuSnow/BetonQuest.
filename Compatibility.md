# Compatibility

BetonQuest can hook into other plugins to extend its functionality. Currently there are 3 plugins: Citizens, Vault and MythicMobs.

## Citizens

If you have this plugin you can use it's NPCs for conversations. I highly recommend you installing it, these NPCs are way more immersive. Having Citizens also allows you to use NPCKill objective.

### NPCKill Objective

**Name**: npckill

**Desc**: NPC Kill objective requires the player to kill an NPC with the given ID. You can also define how many times an NPC has to be killed.

**Instruction**: Right after objective's name there must be na ID of the NPC. You can also add an amount by `amount:`.

**Example**: `npckill 16 amount:3 events:reward tag:citizens`

## Vault

By installing Vault you enable Permission event and Money condition/event.

### Permission Event

**Name**: permission

**Desc**: Adds or removes a permission or a group.

**Instruction**: First argument is `add` or `remove`. It's self-explanatory. Second is `perm` or `group`. It also shouldn't be hard to figure out. Next thing is actual string you want to add/remove. At the end you can also specify world in which you want these permissions. If the world name is ommited then permission/group will be global.

**Example**: `permission remove group bandit world_nether`

### Money Event

**Name**: money

**Desc**: Deposits or withdraws money from player's account.

**Instruction**: There is only one argument, amount of money to modify. It can be positive or negative.

**Example**: `money -100`

### Money Condition

**Name**: money

**Desc**: Checks if the player has specified amount of money

**Instruction**: You can specify only one argument, `amount:`. It's obvious what is it for. It cannot be negative!

**Example**: `money amount:500 --invert`

## MythicMobs

Having MythicMobs allows you to use MythicMobs MobKill objective and MythicMobs SpawnMob event.

### MythicMobs MobKill objective

**Name**: mmobkill

**Desc**: To complete this objective you need to kill specified amount of MythicMobs.

**Instruction**: The first argument must be the mob's internal name (the one defined in MythicMobs' configuration). You can optionally add `amount:` argument to specify how many of these mobs the player needs to kill.

**Example**: `mmobkill amount:2 events:reward tag:mythicmobs`

### MythicMobs SpawnMob Event

**Name**: mspawnmob

**Desc**: Spawn specified amount of MythicMobs at given location.

**Instruction**: The first argument is a location defined like `100;200;300;world`. Second is MythicMobs internal name (the one defined in MythicMobs' configuration) followed by a colon and a level. Third one is amount and it's required!

**Example**: `mspawnmob 100;200;300;world SkeletalKnight:1 5`
