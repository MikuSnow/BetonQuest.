# Conditions List

## Item in Inventory: `item`

This event is met only when player has defined item in his inventory. You specify items in a list separated by commas (without spaces between!) Each item consists of its name and amount, separated by a colon. Amount is optional, so if you specify just item's name the plugin will assume there should be only one item.

**Example** `item emerald:5,gold:10`

## Item in Hand: `hand`

This event is met only when player is holding a specific item in his hand. Amount cannot be set here, though it may be checked with Item in Inventory condition.

**Example** `hand sword`

## Alternative: `or`

Alternative of specified conditions. This means that only one of conditions has to be met in order for alternative to be true. You just define one mandatory argument, condition names separated by commas. `!` prefix works as always.

**Example** `or night,rain,!has_armor`

## Conjunction: `and`

Conjunction of specified conditions. This means that every condition has to be met in order for conjunction to be true. Used only in complex alternatives, as conditions normally work as conjunction. Instruction string is exactly the same as alternative.

**Example** `and has_helmet,has_chestplate,has_leggings,has_boots`

## Location: `location`

It returns true only when player is closer to specified location than given distance. Just one mandatory attribute - location defined exactly as `x;y;z;world;distance`.

**Example** `location 100;200;300;survival_nether;5`

## Health: `health`

Requires player to have equal or more health than specified amount. The only argument is a number (double). Players can have 0 to 20 health by default (there are some plugins and commands which change that).

**Example** `health 5.6`

## Experience: `experience`

This condition is met when player has specified level (default minecraft experience). It is measured by full levels, not experience points. The instruction string must contain an integer argument.

**Example** `experience 30`

## Permission: `permission`

Player must have certain permission for this condition to return true. The instruction string must contain permission node as the required argument.

**Example** `permission essentials.tpa`

## Point: `point`

Requires player to have equal or more points from category than specified. There are two required arguments, first is the category (string), second is count (integer).

**Example** `point beton 20`

## Tag: `tag`

This one requires player to have a tag set by tag event. Together with `!` negation it is one of the most powerful tools when creating conversations. The instruction string must contain tag name.

**Example** `tag quest_completed`

## Armor: `armor`

The armor condition requires player to wear given armor, as an item defined in _items.yml_ file.

**Example** `armor helmet_of_concrete`

## Potion Effect: `effect`

To meet this condition player must be under specified potion effect. There is only one argument and it takes values from this page: [potion types](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/potion/PotionEffectType.html).

**Example** `effect SPEED`

## Time: `time`

There must be specific time for this condition to return true. You need to specify two hour numbers separated by dash. These number are normal 24-hour format hours. The first must be smaller than the second. If you want to achieve time period between 23 and 2 you need to invert the outcome.

**Example** `time 2-23`

## Weather: `weather`

There must be specific weather for this condition to return true. There are three possible options: sun, rain and storm. Note that `/toggledownfall` does not change the weather, it just does what the name suggests: toggles downfall. The rain toggled off will still be rain! Use `/weather clear` instead.

**Example** `weather sun`

## Height: `height`

This condition requires player to be _below_ specific Y height. The required argument is a number or a location (for example 100;200;300;world). In case of location it will take the height from it and use it as regular height.

**Example** `height 16`

## Armor Rating: `rating`

This one requires player to wear armor which gives him specified amount of protection (armor icons). The first and only argument should be an integer. One armor rating point is equal to half armor icon in-game (10 means half of the bar filled).

**Example** `rating 10`

## Random: `random`

This condition returns true randomly. There is one argument: two positive numbers like `5-12`. They mean something like that: "It will be true 5 times out of 12".

**Example**: `random 12-100`

## Sneaking: `sneak`

Sneak condition is only true when the player is sneaking. This would probably be useful for creating traps, I'm not sure. There are no arguments for this one.

**Example**: `sneak`

## Journal entry: `journal`

This condition will return true if the player has specified entry in his journal (internal name of the entry, like in _journal.yml_). The only argument is name of the entry.

**Example**: `journal wood_started`

## Test for block: `testforblock`

This condition is met if the block at specified location matches the given material. First argument is a location, for example `100;200;300;world`, and the second one is material of the block to check against, from [this list](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html).

**Example**: `testforblock 100;200;300;world STONE`

## Empty inventory slots: `empty`

To meet this condition the player has to have specified amount of empty slots in his inventory.

**Example**: `empty 5`

## Party: `party`

To see details about parties read "Party" chapter in **Other important stuff** section. This condition takes three optional arguments: `every:`, `any:` and `count:`. Every is a list of conditions that must be met by every player in the party. Any is a list of conditions that each must be met by at least one player in a party. Count is just a number, minimal amount of players in the party.

**Example**: `party 10 has_tag1,!has_tag2 every:some_item any:some_location,some_other_item count:5`

## Monsters in area: `monsters`

This condition will return true only if there is a specified amount (or more) of specified mobs in the specified area. There are two required arguments - monsters and location. Monsters are defined as a list separated by commas. Each mob type (taken from [here](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/EntityType.html)) can have additional `:amount` suffix, for example `ZOMBIE:5,SKELETON:2` means 5 or more zombies and 2 or more skeletons. The location is specified as `100;200;300;world;10`, where last number is a range aroung the location in which the mobs will be looked for. You can also specify additional `name:` argument, with the name of the required mob. Replace all spaces with `_` here.

**Example**: `monsters ZOMBIE:2 100;200;300;world;10 name:Deamon`
