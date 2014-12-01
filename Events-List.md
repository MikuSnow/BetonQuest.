Events List
===============

Message
---------------

**Name**: message

**Desc**: This event simply displays a message to player.

**Instruction**: You just pass the message right after event name. `%player%` will be replaced with player's name, and all & color codes are respected.

**Example**: `message &4You are banned!`

Command
---------------

**Name**: command

**Desc**: Runs specified command from console.

**Instruction**: You just pass the command without leading slash. All `%player%` are replaced with player's name.

**Example**: `command ban %player%`

Teleport
---------------

**Name**: teleport

**Desc**: Teleports player to specified location, with or without head rotation.

**Instruction**: The first and only argument must be location, created with following syntax: `100;200;300;world` or `100;200;300;world;90;45` where the first 3 numbers are coordinates (double), `world` is name of the world and last to numbers are yaw and pitch respectively (float).

**Example**: `teleport 123;32;-789;world_the_nether;180;45`

Point
---------------

**Name**: point

**Desc**: Gives the player specified amount of points in given category. Amount can be negative to subtract points.

**Instruction**: First argument after event name must be category, and second amount of points to give.

**Example**: `point npc_attitude 10`

Tag
---------------

**Name**: tag

**Desc**: This event adds (or removes) a tag to player. This, along with `--inverted` argument, is one of the most powerful tools for creating dynamic conversations.

**Instruction**: The first argument after event's name must be `add` or `del`. It works as it sounds. Next goes tag string. It can't contain spaces (though _ is fine).

**Example**: `tag add quest_started`

Objective
---------------

**Name**: objective

**Desc**: Creates new objective defined in objectives.yml

**Instruction**: The first and only argument is name of objective defined in objectives.yml

**Example**: `objective woodcutting`

Delete Objective
---------------

**Name**: delete

**Desc**: Deletes objective with given tag. If player has more objectives of the same tag all of them will be deleted.

**Instruction**: Just like the objective event.

**Example**: `delete woodcutting`

Journal
---------------

**Name**: journal

**Desc**: Adds an entry to player’s journal. Entries are defined in `journal.yml`

**Instruction**: The only argument is name of the entry.

**Example**: `journal quest_started`

Lightning
---------------

**Name**: lightning

**Desc**: Strikes a lightning at given location.

**Instruction**: The only argument is location formatted like this: `100;200;300;world`

**Example**: `lightning 100;64;-100;survival`

Explosion
---------------

**Name**: explosion

**Desc**: Creates an explosion. It can make fire and destroy blocks. You can also define power, so be careful not to blow your server away. Default TNT power is 4, while Wither on creation is 7.

**Instruction**: First argument can be 0 or 1 and states if explosion will generate fire (like Ghast’s fireball). Second is also 0 or 1 but this defines if block will be destroyed or not. Third argument is the power (float number). At the end (4th attribute) there is location, formatted as that in lightning event.

**Example**: `explosion 0 1 4 100;64;-100;survival`

Give Items
---------------

**Name**: give

**Desc**: Gives player items, exactly as /give command. Support custom names, lore and enchantments.

**Instruction**: Defining instruction string is the same as in Item condition.

**Example**: `give type:EMERALD amount:120 lore:Beton;reward name:Money`

Take Items
---------------

**Name**: take

**Desc**: Removes items from player’s inventory. It should be used with proper condition. Beware using this in conversations on selecting an option, as the player can drop items before selecting the option and pickup them after the event fires. Always validate it on NPC’s reaction!

**Instruction**: Defining instruction string is the same as in give event.

**Example**: `take type:EMERALD amount:120 lore:Beton;reward name:Money`

Potion Effect
---------------

**Name**: effect

**Desc**: Adds a specified potion effect to player.

**Instruction**: First argument is potion type. You can find all available types [here](http://jd.bukkit.org/rb/apidocs/org/bukkit/entity/EntityType.html). Second is integer defining how long the effect will last in seconds. Third argument, also integer, defines level of the effect (1 means first level). You can also add `--ambient` parameter to make potion particles appear more invisible (just like beacon effects).

**Example**: `effect ABSORPTION 120 1 --ambient`

Conversation
---------------

**Name**: conversation

**Desc**: Starts a conversation at location of the player.

**Instruction**: The only argument is ID of the conversation.

**Example**: `conversation village_smith`

Kill
---------------

**Name**: kill

**Desc**: Kills the player.

**Instruction**: Nothing else.

**Example**: `kill`

Spawn Mob
---------------

**Name**: spawn

**Desc**: Spawns specified amount of mobs of given type at the location.

**Instruction**: First argument is a location defined as in explosion event. Next is type of mobs as in Mob Kill objective. The last, third argument is integer for amount of mobs to be spawned.

**Example**: `spawn 107;66;242;world ZOMBIE 5`

Time
---------------

**Name**: time

**Desc**: Sets or adds time.

**Instruction**: The only argument is time to be set (integer) or time to be added (integer prefixed with +), in 24 hours format. Subtracting time is done by adding more time (if you think of this, it actually makes sense). Minutes can be achieved with floating point.

**Example**: `time +6`

Weather
---------------

**Name**: weather

**Desc**: Sets weather.

**Instruction**: The argument is `sun`, `rain` or `storm`.

**Example**: `weather rain`

Folder
-----------------

**Name**: folder

**Desc**: It's something like a container for multiple events. You can use it to clarify your code. It also features optional delay measured in seconds. Beware though, it's not persistent. If the player leaves the game before that time events will not fire. You probably shouldn't use it to give them items or tags.

**Instruction**: There are two arguments, `delay:` and `events:`. Delay is a number of seconds and it's optional (leaving it blank is the same as `events:0`, and events is a list of event IDs separated by colons.

**Example**: `folder delay:5 events:event1,event2,event3`