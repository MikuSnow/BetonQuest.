# Compatibility

BetonQuest can hook into other plugins to extend its functionality. Currently there are 3 plugins: Citizens, Vault and MythicMobs.

## [Citizens](http://dev.bukkit.org/bukkit-plugins/citizens/)

If you have this plugin you can use it's NPCs for conversations. I highly recommend you installing it, these NPCs are way more immersive. Having Citizens also allows you to use NPCKill objective.

### NPCKill objective: `npckill`

NPC Kill objective requires the player to kill an NPC with the given ID. You can also define how many times an NPC has to be killed. Right after objective's name there must be na ID of the NPC. You can also add an amount by `amount:`.

**Example**: `npckill 16 amount:3 events:reward`

### NPCInteract objective: `npcinteract`

The player has to right-click on the NPC with specified ID. It can also optionally cancel the action, so the conversation won't start. The first argument is number (ID of the NPC), and the second is optional `cancel`.

**Example**: `npcinteract 3 cancel conditions:sneak events:steal`

## [Vault](http://dev.bukkit.org/bukkit-plugins/vault/)

By installing Vault you enable Permission event and Money condition/event.

### Permission event: `permission`

Adds or removes a permission or a group. First argument is `add` or `remove`. It's self-explanatory. Second is `perm` or `group`. It also shouldn't be hard to figure out. Next thing is actual string you want to add/remove. At the end you can also specify world in which you want these permissions. If the world name is ommited then permission/group will be global.

**Example**: `permission remove group bandit world_nether`

### Money event: `money`

Deposits, withdraws or multiplies money on player's account. There is only one argument, amount of money to modify. It can be positive, negative or start with an asterisk for multiplication.

**Example**: `money -100`

### Money condition: `money`

Checks if the player has specified amount of money. You can specify only one argument, amount integer. It cannot be negative!

**Example**: `money 500`

### Money variable: `money`

There is only one argument in this variable, `amount` for showing money amount or `left:` followed by a number for showing the difference between it and amount of money.

**Example**: `%money.left:500%`

## [MythicMobs](http://dev.bukkit.org/bukkit-plugins/mythicmobs/)

Having MythicMobs allows you to use MythicMobs MobKill objective and MythicMobs SpawnMob event.

### MythicMobs MobKill objective: `mmobkill`

To complete this objective you need to kill specified amount of MythicMobs. The first argument must be the mob's internal name (the one defined in MythicMobs' configuration). You can optionally add `amount:` argument to specify how many of these mobs the player needs to kill. You can also add "notify" keyword if you want to display to players the amount of mobs left to kill.

**Example**: `mmobkill SkeletalKnight amount:2 events:reward`

### MythicMobs SpawnMob event: `mspawnmob`

Spawn specified amount of MythicMobs at given location. The first argument is a location defined like `100;200;300;world`. Second is MythicMobs internal name (the one defined in MythicMobs' configuration) followed by a colon and a level. Third one is amount and it's required!

**Example**: `mspawnmob 100;200;300;world SkeletalKnight:1 5`

## [Skript](http://dev.bukkit.org/bukkit-plugins/skript/)

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

## [WorldGuard](http://dev.bukkit.org/bukkit-plugins/worldguard/)

### WorldGuard Region objective: `region`

To complete this objective you need to enter WorldGuard region with specified name. The only argument in instruction string is name of the region.

**Example**: `region beton events:kill`

### WorldGuard Region condition: `region`

This condition is met when the player is inside the specified region. The only argument is the name of the region.

**Example**: `region beton`

## [EffectLib](http://dev.bukkit.org/bukkit-plugins/effectlib/)

If you install this plugin on your server you will be able to set a particle effect on NPCs with conversations and use `particle` event.

You can control the behaviour of particles around the NPCs in _config.yml_ file, in `effectlib_npc_effect` section. All options here are described on the EffectLib page, except for `delay`. This option controls how often the effect is displayed (in seconds). The effect will be fired from the exact location of the NPC, upwards.

If you don't want to use particle effects on your NPCs just add `disabled: 'true'` in the `effectlib_npc_effect` section.

### EffectLib event: `particle`

This event will load an effect defined in `effects` section in _main.yml_ file. The only argument is the name of the effect. You can optionally add `loc:` argument followed by a location written like `100;200;300;world;180;-90`.

**Example in _main.yml_**:

    effects:
      beton:
        class: HelixEffect
        iterations: 100
        particle: smoke
        helixes: 5
        circles: 20
        grow: 3
        radius: 30

**Example**: `particle beton`

## [PlayerPoints](http://dev.bukkit.org/bukkit-plugins/playerpoints/)

### PlayerPoints event: `playerpoints`

This event simply adds, removes or multiplies points in the PlayerPoints plugin. The only argument is a number, it can be positive, negative or prefixed with an asterisk for multiplication.

**Example**: `playerpoints *2`

### PlayerPoints condition: `playerpoints`

This condition simply checks if the player has specified amount of points in the PlayerPoints plugin. The only argument is a number.

**Example**: `playerpoints 100`

## [Heroes](http://dev.bukkit.org/bukkit-plugins/heroes/)

When you install Heroes, all kills done via this plugin's skills will be counted in MobKill objectives.

### Heroes Experience event: `heroesexp`

This event simply gives the player specified amount of Heroes experience. The first argument is either `primary` or `secondary` and it means player's class. Second one is the amount of experience to add.

**Example**: `heroesexp primary 1000`

### Heroes Class condition: `heroesclass`

This condition checks the classes of the player. The first argument must be `primary`, `secondary` or `mastered`. Second is the name of a class or `any`. You can optionally specify `level:` argument followed by the required level of the player.

**Example**: `heroesclass mastered warrior`

### Heroes Skill condition: `heroesskill`

This condition checks if the player can use specified skill. The first argument is the name of the skill.

**Example**: `heroesskill charge`

## [Magic](http://dev.bukkit.org/bukkit-plugins/magic/)

### Wand condition: `wand`

This condition can check wands. The first argument is either `hand`, `inventory` or `lost`. If you choose `lost`, the condition will check if the player has lost a wand. If you choose `hand`, the condition will check if you're holding a wand in your hand. `inventory` will check your whole inventory instead of just the hand. In case of `hand` and `inventory` arguments you can also add optional `name:` argument followed by the name of the wand (as defined in _wands.yml_ in Magic plugin) to check if it's the specific type of the wand. You can also use optional `spells:` argument, followed by a list of spells separated with a comma. Each spell in this list can have defined minimal level required, after a colon.

**Example**: `wand hand name:master spells:flare,missile:2`

## [Denizen](http://dev.bukkit.org/bukkit-plugins/denizen/)

### Script event: `script`

With this event you can fire Denizen task scripts. Don't confuse it with `skript` event, these are different. The first and only argument is the name of the script.

**Example**: `script beton`

## [SkillAPI](http://dev.bukkit.org/bukkit-plugins/skillapi/)

### Class condition: `skillapiclass`

This condition checks if the player has specified class or a child class of the specified one. The first argument is simply the name of a class. You can add `exact` argument if you want to check for that exact class, without checking child classes.

**Example**: `skillapiclass warrior`

### Level condition: `skillapilevel`

This condition checks if the player has specified or greater level is the specified class. The first argument is class name, the second one is the required level.

**Example**: `skillapilevel warrior 3`

## [Quests](http://dev.bukkit.org/bukkit-plugins/quests/)

Quests is another questing plugin, which offers very simple creation of quests. If you don't want to spend a lot of time to write advanced quests in BetonQuest but you need a specific thing from this plugin you can use Custom Event Reward or Custom Condition Requirement. Alternatively, if you have a lot of quests written in Quests, but want to integrate them with the conversation system, you can use `quest` event and `quest` condition.

### Event Reward (Quests)

When adding rewards to a quest or a stage, choose "Custom reward" and then select "BetonQuest event". Now specify event's name and it's package (like `package.eventName`). Quests will fire BetonQuest event when this reward will run.

### Condition Requirement (Quests)

When adding requirements to a quest, choose "Custom requirement" and then select "BetonQuest condition". Now specify condition's name and it's package (like `package.conditionName`). Quests will check BetonQuest condition when starting the quest.

### Quest event: `quest` (BetonQuest)

This event will start the quest for the player. The first argument must be the name of the quest, as defined in `name` option in the quest. If the name contains any spaces replace them with `_`. You can optionally add `check-requirements` argument if you want the event to respect this quest's requirements (otherwise the quest will be forced to be started).

**Example**: `quest stone_miner check-requirements`

### Quest condition: `quest` (BetonQuest)

This condition is met when the player has completed the specified quest. The first and only argument is the name of the quest. It it contains any spaces replace them with `_`.

**Example**: `quest stone_miner`
