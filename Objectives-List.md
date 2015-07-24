# Objectives List

## Location: `location`

This objective completes when player moves in specified range of specified location and meets all conditions. The first argument after objective's name must be location written like `100;200;300;world;5` where 100 is X coordinate, 200 is Y, 300 is Z, world is name of a world and 5 is required range. All conditions and events must be passed after location argument. Coordinates must be valid doubles (floating point must be dot) and world must be name of a loaded world.

**Example**: `location 100;200;300;world;5 condition:test1,!test2 events:test1,test2`

## Block: `block`

To complete this objective player must break or place specified amount of blocks. First argument after name is type of the block and data value after a colon (WOOD:2 means birch wooden planks). You can find possible types at Bukkit reference page there: [material types](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html). Next is amount. It can be more than 0 for placing and less than 0 for destroying. You can also use `notify` keyword to display messages to the player each time he updates amount of blocks.

**Example**: `block LOG:2 -16 events:reward notify`

## Mob Kill: `mobkill`

The player must kill specified amount of mobs You must specify mob type first and then amount. You can find possible mob types here: [mob types](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/EntityType.html). Additionally you can specify names for mobs with `name:Uber_Zombie`, so only killing properly named mobs counts. All `_` are replaced with spaces, so in this example you would have to kill 5 zombies with "Uber Zombie" above their heads. You can also specify `notify` keyword to display messages to the player each time he kills a mob.

**Example**: `mobkill ZOMBIE 5 name:Uber_Zombie conditions:night`

## Action: `action`

This objective completes when player clicks on given block type. This can be further limited by location condition and item in hand condition. First argument is type of the click, it can be right, left or any. Next is block type, optionally with data value after colon. You can also specify `loc:` argument, followed by standard location format. It will define where the clicked block needs to be, as opposed to "where you must be" in location condition. If you add argument `cancel`, the click will be canceled (chest will not open etc.)

**Example**: `action right DOOR:1 conditions:holding_key loc:100;200;300;world`

## Death: `die`

Death objective completes when the player dies meeting all conditions. You can optionally cancel death with `cancel’ argument. It will heal player and optionally teleport him to respawn location. There can be two arguments: `cancel`, which is optional, and `respawn:`, which is also optional and only used if there is the `cancel` argument set. You can add them right after type of objective.

**Example**: `die cancel respawn:100;200;300;world;90;0 events:teleport`

## Crafting: `craft`

To complete this objective player must craft specific item. First argument is material name followed by data value separated by a colon. Next is amount (integer).

**Example**: `craft WOOD:0 10 events:reward`

## Smelting: `smelt`

To complete this objective player must smelt specific item. Note that you must define item as output from furnace, not the ingredient. This one does not support data values (it doesn’t have to). First argument is material name. Next is amount (integer).

**Example**: `smelt IRON_INGOT 5 events:reward`

## Taming: `tame`

To complete this objective player must tame some amount of mobs. valid mob types are: WOLF, OCELOT and HORSE First argument is type, next is amount.

**Example**: `tame WOLF 2 events:wolfs_tamed`

## Delay: `delay`

This objective is just a long, persistent delay for firing events. It will run only after certain amount of time (measured in minutes) and only when player is online and meets all conditions. If a player is offline at that time it will just wait for them to log in. It is not 100% accurate though, as it can run up to a minute after the required amount of time. You should use it for example to delete tags so the player can complete quests multiple times. First argument is number of minutes. The rest is just like in other objectives.

**Example**: `delay 1440 events:!event1,event2`

## Arrow Shooting: `arrow`

To complete this objective the player needs to shoot the arrow into the target. There is only one argument, location of the target and precision: `100.5;200.5;300.5;world;1.1`, where the last number (1.1 in this case) is precision. Note that the position of an arrow after hit is on the wall of a _full_ block, which means that shooting not full blocks (like heads) won't give accurate results.

**Example**: `arrow 100.5;200.5;300.5;world;1.1 events:reward conditions:correct_player_position`

## Experience: `experience`

This objective can by completed by reaching specified level (default Minecraft experience, whole levels). The conditions are checked when the player levels up, so if they are not met the first time, the player will have to meet them and levelup again. Instruction string consists only from integer - level to reach.

**Example**: `experience 25 events:reward`

## Step on pressure plate: `step`

To complete this objective the player has to step on pressure plate at given location. The type of plate does not matter. The first and only required argument is a location formatted as `100;200;300;world`. If the pressure plate is not present at that location, the objective will not be completable.

**Example**: `step 100;200;300;world events:done`
