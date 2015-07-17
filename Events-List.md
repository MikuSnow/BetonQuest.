# Events List

## Message: `message` _static_

This event simply displays a message to player. You just pass the message right after event name. `%player%` will be replaced with player's name, and all & color codes are respected. You can add additional translations by starting them with `{lang}` argument, just like in the example. The player will see his language or the default one if it's not defined.

**Example**: `message {en} &4You are banned! {pl} &4Jestes zbanowany! {de}&4Ich weiß nicht.`

## Command: `command` _persistent_, _static_

Runs specified command from console. You just pass the command without leading slash. All `%player%` are replaced with player's name. You can define additional commands by separating them wit `|` character.

**Example**: `command kill %player%|ban %player%`

## Teleport: `teleport`

Teleports player to specified location, with or without head rotation. It will also end the conversation, if the player has one active. The first and only argument must be location, created with following syntax: `100;200;300;world` or `100;200;300;world;90;45` where the first 3 numbers are coordinates (double), `world` is name of the world and last to numbers are yaw and pitch respectively (float).

**Example**: `teleport 123;32;-789;world_the_nether;180;45`

## Point: `point` _persistent_

Gives the player specified amount of points in given category. Amount can be negative to subtract points. First argument after event name must be category, and second amount of points to give.

**Example**: `point npc_attitude 10`

## Tag: `tag` _persistent_

This event adds (or removes) a tag to player. This, along with `!` negation, is one of the most powerful tools for creating dynamic conversations. The first argument after event's name must be `add` or `del`. It works as it sounds. Next goes tag string. It can't contain spaces (though _ is fine). Additional tags can be added, separated by commas (without spaces).

**Example**: `tag add quest_started,new_entry`

## Objective: `objective` _persistent_

Manages the objectives. Syntax is `objective <action> name`, where <action> can be "start", "delete" or "complete". Name is the name of the objective, as defined in _objectives.yml_.

**Example**: `objective start wood`

## Delete Objective: `delete` _persistent_

Deletes objective with given tag. If player has more objectives of the same tag all of them will be deleted. Just like the objective event.

**Example**: `delete woodcutting`

## Journal: `journal`

Adds an entry to player’s journal. Entries are defined in `journal.yml` The only argument is name of the entry.

**Example**: `journal quest_started`

## Lightning: `lightning` _static_

Strikes a lightning at given location. The only argument is location formatted like this: `100;200;300;world`

**Example**: `lightning 100;64;-100;survival`

## Explosion: `explosion` _static_

Creates an explosion. It can make fire and destroy blocks. You can also define power, so be careful not to blow your server away. Default TNT power is 4, while Wither on creation is 7. First argument can be 0 or 1 and states if explosion will generate fire (like Ghast’s fireball). Second is also 0 or 1 but this defines if block will be destroyed or not. Third argument is the power (float number). At the end (4th attribute) there is location, formatted as that in lightning event.

**Example**: `explosion 0 1 4 100;64;-100;survival`

## Give Items: `give`

Gives the player predefined items. They are specified exactly as in `item` condition - list separated by commas, every item can have amount separated by colon. Default amount is 1. If the player doesn't have required space in the inventory, the items are dropped on the ground, unless they are quest items. Then they will be put into the backpack. You can also specify `notify` keyword to display a simple message to the player about receiving items.

**Example**: `give emerald:5,emerald_block:9`

## Take Items: `take`

Removes items from player’s inventory or backpack (in that order). If the items aren't quest items don't use `take` event with player options in conversations! The player can drop items before selecting the option and pickup them after the event fires. Validate it on NPC’s reaction! Defining instruction string is the same as in give event.  You can also specify `notify` keyword to display a simple message to the player about loosing items.

**Example**: `take emerald:120,sword`

## Potion Effect: `effect`

Adds a specified potion effect to player. First argument is potion type. You can find all available types [here](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/EntityType.java). Second is integer defining how long the effect will last in seconds. Third argument, also integer, defines level of the effect (1 means first level). You can also add `--ambient` parameter to make potion particles appear more invisible (just like beacon effects).

**Example**: `effect ABSORPTION 120 1 --ambient`

## Conversation: `conversation`

Starts a conversation at location of the player. The only argument is ID of the conversation. This bypasses the conversation permission!

**Example**: `conversation village_smith`

## Kill: `kill`

Kills the player. Nothing else.

**Example**: `kill`

## Spawn Mob: `spawn` _static_

Spawns specified amount of mobs of given type at the location. First argument is a location defined as in explosion event. Next is [type of the mob](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/EntityType.html). The last, third argument is integer for amount of mobs to be spawned. You can also specify `name:` argument, followed by the name of the mob. All `_` characters will be replaced with spaces.

**Example**: `spawn 107;66;242;world ZOMBIE 5 name:The_Zombie`

## Time: `time`

Sets or adds time. The only argument is time to be set (integer) or time to be added (integer prefixed with +), in 24 hours format. Subtracting time is done by adding more time (if you think of this, it actually makes sense). Minutes can be achieved with floating point.

**Example**: `time +6`

## Weather: `weather`

Sets weather. The argument is `sun`, `rain` or `storm`.

**Example**: `weather rain`

## Folder: `folder` _persistent_, _static_

It's something like a container for multiple events. You can use it to clarify your code. It also features optional delay measured in seconds. It is persistent for events marked as _persistent_, which means that the events will be fired even after the player logs out. Beware though, all conditions are false then the player is offline (even inverted ones), so those events should not be blocked by any conditions! The only required argument is a list of events separated by commas. There are also two optional arguments: `delay:` and `random:`. Delay is a number of seconds and it's optional (leaving it blank is the same as `delay:0`. Random is the amount of events, that will be randomly chosen to fire. If set to 0 or omited, it does nothing (all events will fire).

**Example**: `folder event1,event2,event3 delay:5 random:1`

## Set Block: `setblock` _persistent_, _static_

Sets a block at given location to specified material. Useful for triggering redstone contraptions. There are two required arguments. First is required, and should be  material's name ([List of materials](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html)). Second is a location written like `100;200;300;world` and is also required. Last, optional is `data:` with an integer, which defines block's data value. Default is 0.

**Example**: `setblock REDSTONE_BLOCK 100;200;300;world`

## Damage player: `damage`

Damages the player by specified amount of damage. The only argument is a number (can have floating point).

**Example**: `damage 20`

## Party event: `party`

Runs the specified list of events (third argument) for every player in a party. More info about parties in "Party" chapter in **Other important stuff** section.

**Example**: `party 10 has_tag1,!has_tag2 give_reward`

## Clear mobs: `clear`

This event removes all specified mobs from the specified area. The first required argument is a list of mobs (taken from [here](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/EntityType.html)) separated by commas. Next is location defined as `100;200;300;world;10` where last number is range aroung the location. You can also optionally specify `name:` argument, followed by name which removed mobs must have.

**Example**: `clear ZOMBIE,CREEPER 100;200;300;world;10 name:Monster`
