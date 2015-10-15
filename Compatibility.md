# Compatibility

BetonQuest can hook into other plugins to extend its functionality. Currently there are 3 plugins: Citizens, Vault and MythicMobs.

## Citizens

If you have this plugin you can use it's NPCs for conversations. I highly recommend you installing it, these NPCs are way more immersive. Having Citizens also allows you to use NPCKill objective.

### NPCKill Objective `npckill`

NPC Kill objective requires the player to kill an NPC with the given ID. You can also define how many times an NPC has to be killed. Right after objective's name there must be na ID of the NPC. You can also add an amount by `amount:`.

**Example**: `npckill 16 amount:3 events:reward`

### NPCInteract Objective

The player has to right-click on the NPC with specified ID. It can also optionally cancel the action, so the conversation won't start. The first argument is number (ID of the NPC), and the second is optional `cancel`.

**Example**: `npcinteract 3 cancel conditions:sneak events:steal`

## Vault

By installing Vault you enable Permission event and Money condition/event.

### Permission Event `permission`

Adds or removes a permission or a group. First argument is `add` or `remove`. It's self-explanatory. Second is `perm` or `group`. It also shouldn't be hard to figure out. Next thing is actual string you want to add/remove. At the end you can also specify world in which you want these permissions. If the world name is ommited then permission/group will be global.

**Example**: `permission remove group bandit world_nether`

### Money Event `money`

Deposits or withdraws money from player's account. There is only one argument, amount of money to modify. It can be positive or negative.

**Example**: `money -100`

### Money Condition `money`

Checks if the player has specified amount of money. You can specify only one argument, amount integer. It cannot be negative!

**Example**: `money 500`

## MythicMobs

Having MythicMobs allows you to use MythicMobs MobKill objective and MythicMobs SpawnMob event.

### MythicMobs MobKill objective `mmobkill`

To complete this objective you need to kill specified amount of MythicMobs. The first argument must be the mob's internal name (the one defined in MythicMobs' configuration). You can optionally add `amount:` argument to specify how many of these mobs the player needs to kill.

**Example**: `mmobkill SkeletalKnight amount:2 events:reward`

### MythicMobs SpawnMob Event `mspawnmob`

Spawn specified amount of MythicMobs at given location. The first argument is a location defined like `100;200;300;world`. Second is MythicMobs internal name (the one defined in MythicMobs' configuration) followed by a colon and a level. Third one is amount and it's required!

**Example**: `mspawnmob 100;200;300;world SkeletalKnight:1 5`

## Skript

BetonQuest can also hook into Skript. Firstly, to avoid any confusion, I will refere to everything here by name of the plugin (Skript event is something else than BetonQuest event). Having Skript on your server will enable using BetonQuest events and conditions in scripts, and also trigger them by BetonQuest event.

### Skript event triggered by BetonQuest `skript` event

This entry will describe two things: Skript event and BetonQuest event.

1. **Skript event** - `on [betonquest] event "id"` - this is the line you use in your scripts to trigger the code. `betonquest` part is optional, and `id` is just some string, which must be equal to the one you specified in BetonQuest event.
2. **BetonQuest event** - `skript` - this event will trigger the above Skript event in your scripts. The instruction string accepts only one argument, id of the event. It have to be the same as the one defined in Skript event for it to be triggered.

**Example**: _in your script:_ `on betonquest event "concrete":` _in events.yml:_ `fire_concrete_script: skript concrete`

### Skript condition

You can check BetonQuest conditions in your scripts by using the syntax `player meets [betonquest] condition "id"`. `betonquest` is optional, and `id` is the name of the condition, as defined in _conditions.yml_.

**Example**: _in your script:_ `player meets condition "has_ore"` _in conditions.yml:_ `has_ore: item iron_ore:5`

### Skript event

You can also fire BetonQuest events with scripts. The syntax for Skript effect is `fire [betonquest] event "id" for player`. Everything else works just like in condition above.

**Example**: _in your script:_ `fire event "give_emeralds" for player` _in events.yml:_ `give_emeralds: give emerald:5`

## WorldGuard

### WorldGuard Region objective `region`

To complete this objective you need to enter WorldGuard region with specified name. The only argument in instruction string is name of the region.

**Example**: `region beton events:kill`

### WorldGuard Region condition `region`

This condition is met when the player is inside the specified region. The only argument is the name of the region.

**Example**: `region beton`
