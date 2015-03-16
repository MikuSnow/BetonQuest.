# Events List

## Message: `message`

This event simply displays a message to player. You just pass the message right after event name. `%player%` will be replaced with player's name, and all & color codes are respected.

**Example**: `message &4You are banned!`

## Command: `command` _persistent_

Runs specified command from console. You just pass the command without leading slash. All `%player%` are replaced with player's name.

**Example**: `command ban %player%`

## Teleport: `teleport`

Teleports player to specified location, with or without head rotation. The first and only argument must be location, created with following syntax: `100;200;300;world` or `100;200;300;world;90;45` where the first 3 numbers are coordinates (double), `world` is name of the world and last to numbers are yaw and pitch respectively (float).

**Example**: `teleport 123;32;-789;world_the_nether;180;45`

## Point: `point` _persistent_

Gives the player specified amount of points in given category. Amount can be negative to subtract points. First argument after event name must be category, and second amount of points to give.

**Example**: `point npc_attitude 10`

## Tag: `tag` _persistent_

This event adds (or removes) a tag to player. This, along with `!` negation, is one of the most powerful tools for creating dynamic conversations. The first argument after event's name must be `add` or `del`. It works as it sounds. Next goes tag string. It can't contain spaces (though _ is fine). Additional tags can be added, separated by commas (without spaces).

**Example**: `tag add quest_started,new_entry`

## Objective: `objective` _persistent_

Creates new objective for a player. This is different from other events. The only argument is a full instruction string of the objective. You just type it right after `objective`, without any quotation marks. You can find out how to write instruction strings for objectives [here](https://github.com/Co0sh/BetonQuest/wiki/Objectives-List). If you need to add `event_conditions:` do it at the end of the whole instruction string to avoid errors with parsing the objective.

**Example**: `objective block LOG:2 -16 events:reward tag:beton`

## Delete Objective: `delete` _persistent_

Deletes objective with given tag. If player has more objectives of the same tag all of them will be deleted. Just like the objective event.

**Example**: `delete woodcutting`

## Journal: `journal`

Adds an entry to player’s journal. Entries are defined in `journal.yml` The only argument is name of the entry.

**Example**: `journal quest_started`

## Lightning: `lightning`

Strikes a lightning at given location. The only argument is location formatted like this: `100;200;300;world`

**Example**: `lightning 100;64;-100;survival`

## Explosion: `explosion`

Creates an explosion. It can make fire and destroy blocks. You can also define power, so be careful not to blow your server away. Default TNT power is 4, while Wither on creation is 7. First argument can be 0 or 1 and states if explosion will generate fire (like Ghast’s fireball). Second is also 0 or 1 but this defines if block will be destroyed or not. Third argument is the power (float number). At the end (4th attribute) there is location, formatted as that in lightning event.

**Example**: `explosion 0 1 4 100;64;-100;survival`

## Give Items: `give`

Gives the player predefined items. They are specified exactly as in `item` condition - list separated by commas, every item can have amount separated by colon. Default amount is 1. If the player doesn't have required space in the inventory, the items are dropped on the ground, unless they are quest items. Then they will be put into the backpack.

**Example**: `give emerald:5,emerald_block:9`

## Take Items: `take`

Removes items from player’s inventory or backpack (in that order). If the items aren't quest items don't use `take` event with player options in conversations! The player can drop items before selecting the option and pickup them after the event fires. Validate it on NPC’s reaction! Defining instruction string is the same as in give event.

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

## Spawn Mob: `spawn`

Spawns specified amount of mobs of given type at the location. First argument is a location defined as in explosion event. Next is type of mobs as in Mob Kill objective. The last, third argument is integer for amount of mobs to be spawned.

**Example**: `spawn 107;66;242;world ZOMBIE 5`

## Time: `time`

Sets or adds time. The only argument is time to be set (integer) or time to be added (integer prefixed with +), in 24 hours format. Subtracting time is done by adding more time (if you think of this, it actually makes sense). Minutes can be achieved with floating point.

**Example**: `time +6`

## Weather: `weather`

Sets weather. The argument is `sun`, `rain` or `storm`.

**Example**: `weather rain`

## Folder: `folder` _persistent_

It's something like a container for multiple events. You can use it to clarify your code. It also features optional delay measured in seconds. It is persisten for events marked as _persistent_, which means that the events will be fired even after the player logs out. Beware though, all conditions are false then the player is offline (even inverted ones), so those events should not be blocked by any conditions! There are two arguments, `delay:` and `events:`. Delay is a number of seconds and it's optional (leaving it blank is the same as `delay:0`, and events is a list of event IDs separated by colons.

**Example**: `folder delay:5 events:event1,event2,event3`

## Set Block: `setblock` _persistent_

Sets a block at given location to specified material. Useful for triggering redstone contraptions. There are three arguments. `block:` is required, and should be followed by material's name ([List of materials](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html)). `loc:` is a location written like `100;200;300;world` and is also required. Last, optional is `data:` with an integer, which defines block's data value. Default is 0.

**Example**: `setblock block:REDSTONE_BLOCK loc:100;200;300;world`

## Damage player: `damage`

Damages the player by specified amount of damage. The only argument is a number (can have floating point).

**Example**: `damage 20`
