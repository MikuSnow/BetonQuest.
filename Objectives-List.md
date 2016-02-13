# Objectives List

## Location: `location`

This objective completes when player moves in specified range of specified location and meets all conditions. The first argument after objective's name must be location written like `100;200;300;world;5` where 100 is X coordinate, 200 is Y, 300 is Z, world is name of a world and 5 is required range. All conditions and events must be passed after location argument. Coordinates must be valid doubles (floating point must be dot) and world must be name of a loaded world.

Location objective contains one property, `location`. It's a string formatted like `X: 100, Y: 200, Z:300`. It does not show the radius.

**Example**: `location 100;200;300;world;5 condition:test1,!test2 events:test1,test2`

## Block: `block`

To complete this objective player must break or place specified amount of blocks. First argument after name is type of the block and data value after a colon (WOOD:2 means birch wooden planks). You can find possible types at Bukkit reference page there: [material types](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html). Next is amount. It can be more than 0 for placing and less than 0 for destroying. You can also use `notify` keyword to display messages to the player each time he updates amount of blocks.

This objective has two properties, `amount` and `left`. Amount is current amount of blocks in the objective, left is amount needed to complete the objective. Note that it may sometimes be negative!

**Example**: `block LOG:2 -16 events:reward notify`

## Mob Kill: `mobkill`

The player must kill specified amount of mobs You must specify mob type first and then amount. You can find possible mob types here: [mob types](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/EntityType.html). Additionally you can specify names for mobs with `name:Uber_Zombie`, so only killing properly named mobs counts. All `_` are replaced with spaces, so in this example you would have to kill 5 zombies with "Uber Zombie" above their heads. You can also specify `notify` keyword to display messages to the player each time he kills a mob.

This objective also has two properties, `amount` and `left`. Amount is current amount of killed mobs, left is amount needed to complete the objective.

**Example**: `mobkill ZOMBIE 5 name:Uber_Zombie conditions:night`

## Action: `action`

This objective completes when player clicks on given block type. This can be further limited by location condition and item in hand condition. First argument is type of the click, it can be right, left or any. Next is block type, optionally with data value after colon. You can also specify `loc:` argument, followed by standard location format with additional range number, just like in location objective. It will define where the clicked block needs to be, as opposed to "where you must be" in location condition. If you add argument `cancel`, the click will be canceled (chest will not open etc.)

Action objective contains one property, `location`. It's a string formatted like `X: 100, Y: 200, Z:300`. It does not show the radius.

**Example**: `action right DOOR:1 conditions:holding_key loc:100;200;300;world;5`

## Death: `die`

Death objective completes when the player dies meeting all conditions. You can optionally cancel death with `cancel’ argument. It will heal player and optionally teleport him to respawn location. There can be two arguments: `cancel`, which is optional, and `respawn:`, which is also optional and only used if there is the `cancel` argument set. You can add them right after type of objective.

**Example**: `die cancel respawn:100;200;300;world;90;0 events:teleport`

## Crafting: `craft`

To complete this objective player must craft specified item. First argument is material name followed by data value separated by a colon. Next is amount (integer).

Crafting objective has two properties, `amount` and `left`. Amount is current amount of crafted items and left is amount needed to complete the objective.

**Example**: `craft WOOD:0 10 events:reward`

## Smelting: `smelt`

To complete this objective player must smelt specified item. Note that you must define item as output from furnace, not the ingredient. This one does not support data values (it doesn’t have to). First argument is material name. Next is amount (integer).

Smelting has the same properties as crafting objective.

**Example**: `smelt IRON_INGOT 5 events:reward`

## Taming: `tame`

To complete this objective player must tame some amount of mobs. valid mob types are: WOLF, OCELOT and HORSE First argument is type, next is amount.

Taming has the same properties as mob kill objective.

**Example**: `tame WOLF 2 events:wolfs_tamed`

## Delay: `delay`

This objective is just a long, persistent delay for firing events. It will run only after certain amount of time (measured in minutes) and only when player is online and meets all conditions. If a player is offline at that time it will just wait for them to log in. It is not 100% accurate though, as it can run up to a minute after the required amount of time. You should use it for example to delete tags so the player can complete quests multiple times. First argument is number of minutes. The rest is just like in other objectives.

Delay has two properties, `left` and `date`. The first one will show how much time needs to pass before the delay is completed (i.e. `23 days, 5 hours and 45 minutes`), the second one will show a date of completing the objective formatted using `date_format` setting in _config.yml_ (it will look like the one above every journal entry).

**Example**: `delay 1440 events:!event1,event2`

## Arrow Shooting: `arrow`

To complete this objective the player needs to shoot the arrow into the target. There is only one argument, location of the target and precision: `100.5;200.5;300.5;world;1.1`, where the last number (1.1 in this case) is precision. Note that the position of an arrow after hit is on the wall of a _full_ block, which means that shooting not full blocks (like heads) won't give accurate results.

**Example**: `arrow 100.5;200.5;300.5;world;1.1 events:reward conditions:correct_player_position`

## Experience: `experience`

This objective can by completed by reaching specified level (default Minecraft experience, whole levels). The conditions are checked when the player levels up, so if they are not met the first time, the player will have to meet them and levelup again. Instruction string consists only from integer - level to reach.

**Example**: `experience 25 events:reward`

## Step on pressure plate: `step`

To complete this objective the player has to step on pressure plate at given location. The type of plate does not matter. The first and only required argument is a location formatted as `100;200;300;world`. If the pressure plate is not present at that location, the objective will not be completable.

Step objective contains one property, `location`. It's a string formatted like `X: 100, Y: 200, Z:300`. It shows an exact location of the pressure plate.

**Example**: `step 100;200;300;world events:done`

## Logout: `logout`

To complete this objective the player simply needs to leave the server. Keep in mind that running `folder` event here will make it run in "persistent" mode, since the player is offline on the next tick.

**Example**: `logout events:delete_objective`

## Password: `password`

This objective requires the player to type the password in the chat. The first argument is the password. All `_` characters are replaced with spaces. It's checked with [regular expressions](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html) (if your password will be `^beton.*beton$` the objective will accept all passwords that starts and ends with `beton` word (`^` represents beginning of a string, `.` represents any character, `*` allows the previous character (in this case any) repeat any number of times, and `$` means end of the string), but you can also use something like `beton` - it will work). If you want the objective to ignore case of the letters you can add optional `ignoreCase` argument. For this to work your regular expression needs to use lower case letters. To answer, the player needs to type (in his language, configurable in _messages.yml_) `password: here goes player's guess`. If he fails, the message will not be displayed in the chat.

**Example**: `password beton ignoreCase events:message,reward`

## Fishing: `fish`

Requires the player to catch a fish. It doesn't have to be a fish, it can also be a treasure or junk. The first argument is [material](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html) name of the item to catch, optionally with data value after a colon. Second argument must be amount of fish to catch. You can also add `notify` argument if you want to display progress.

Fishing has the same properties as mob kill objective.

**Example**: `fish raw_fish:1 5 notify events:tag_fish_caught`

## Sheep shearing: `shear`

To complete this objective the player has to shear specified amount of sheep, optionally with specified color and/or name. The first, required argument is amount (integer). Optionally, you can add `name:` argument with the name and `color:` with [color name](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/DyeColor.html).

Sheep shearing has the same properties as mob kill objective.

**Example**: `shear 1 name:Bob color:black`

## Enchant item: `enchant`

This objectie is completed when the player enchants specified item with specified enchantment. The first argument is an item name, as defined it _items.yml_. Second one is the [enchantment](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/enchantments/Enchantment.html) and a level, separated with a colon.

**Example**: `enchant sword damage_all:1 events:reward`

## Put items in a chest: `chestput`

This objective requires the player to put specified items in a specified chest. First argument is a location of the chest, defined as `100;200;300;world`, second argument is a list of items (from _items.yml_ file), separated with a comma. You can also add amount of items after a colon. The items will be removed upon completing the objective unless you add `items-stay` optional argument.

**Example**: `chestput 100;200;300;world emerald:5,sword events:tag,message`

## Potion brewing: `potion`

To complete this objective the player needs to brew specified amount of specified potions. The first argument is a type of potion, as a number (you can find it by pressing F3+H and hovering your mouse cursor over the potion item - it will show something like `#0373/8225`, here `8225` means Regeneration Potion II). Second argument is amount of potions. You can optionally add `effects:` arguments if your server has custom potion brewing (if you can brew a potion with custom effects like i.e. blindness, mcMMO has such feature). This argument should be a list of effects, separated with commas, each effect should consist of [effect type](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/potion/PotionEffectType.html) and duration in seconds, separated with a colon. You can optionally add `notify` argument to make the objective display progress to players.

The brewing will be accepted if the player was the last one to click the ingredient slot in the brewing stand and there were no matching potions there already.

Potion objective has `amount` and `left:` properties.

**Example**: `potion 8225 3 events:add_tag`

**Example**: `potion 8225 3 effects:blindness:20,wither:10 events:give_item`
