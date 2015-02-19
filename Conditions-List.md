# Conditions List

## Item in Inventory: `item`

This event is met only when player has defined item in his inventory. You specify items in a list separated by commas (without spaces between!) Each item consists of its name and amount, separated by a colon. Amount is optional, so if you specify just item's name the plugin will assume there should be only one item.

**Example** `item emerald:5,gold:10`

## Item in Hand: `hand`

This event is met only when player is holding a specific item in his hand. Amount cannot be set here, though it may be checked with Item in Inventory condition.

**Example** `hand item:sword`

## Alternative: `or`

Alternative of specified conditions. This means that only one of conditions has to be met in order for alternative to be true. You just define one argument, `conditions:` followed by condition names separated by commas. `!` prefix works as always.

**Example** `or conditions:night,rain,!has_armor`

## Conjunction: `and`

Conjunction of specified conditions. This means that every condition has to be met in order for conjunction to be true. Used only in complex alternatives, as conditions normally work as conjunction. Instruction string is exactly the same as alternative.

**Example** `and conditions:has_helmet,has_chestplate,has_leggings,has_boots`

## Location: `location`

It returns true only when player is closer to specified location than given distance. Just one attribute, specified as `loc:` and location defined exactly as `x;y;z;world;distance`.

**Example** `location loc:100;200;300;survival_nether;5`

## Health: `health`

Requires player to have equal or more health than specified amount. Only one attribute, `health:` followed by a number (double). Players can have 0 to 20 health by default (there are some plugins and commands which change that).

**Example** `health health:5.6`

## Experience: `experience`

This condition is met when player has specified level (default minecraft experience). It is measured by full levels, not experience points. The instruction string must contain argument `exp:X` where X is integer, eg. `exp:20`.

**Example** `experience exp:30`

## Permission: `permission`

Player must have certain permission for this condition to return true. The instruction string must contain argument `perm:permission.node`.

**Example** `permission perm:essentials.tpa`

## Point: `point`

Requires player to have equal or more points from category than specified. There are two arguments, `category:` followed by a string and `count:` followed by an integer.

**Example** `point category:beton count:20 --inverted`

## Tag: `tag`

This one requires player to have a tag set by tag event. Together with `!` negation it is one of the most powerful tools when creating conversations. The instruction string must contain `tag:some_text` argument, where some_text it's tag string.

**Example** `tag tag:quest_completed`

## Armor: `armor`

The armor condition requires player to wear given armor type, optionally with enchantments of equal or greater power than specified. There can be 3 arguments: `type:` is type of armor (possible options are helmet, chestplate, leggings and boots), `material:` is the material of armor (possible options are leather, gold, chainmail, iron and diamond) and `enchants:` is a list of enchantments defined exactly as in item condition.

**Example** `armor type:helmet material:iron enchants:PROTECTION_ENVIRONMENTAL:2,THORNS:1`

## Potion Effect: `effect`

To meet this condition player must be under specified potion effect. There is only one argument, `type:`, and it takes values from this page: [potion types](https://github.com/Co0sh/Bukkit-JavaDoc/blob/master/src/main/java/org/bukkit/potion/PotionEffectType.java).

**Example** `effect type:SPEED`

## Time: `time`

There must be specific time for this condition to return true. You need to specify `time:` attribute followed by two hour numbers separated by dash. These number are normal 24-hour format hours. The first must be smaller than the second. If you want to achieve time period between 23 and 2 you need to invert outcome.

**Example** `time time:2-23`

## Weather: `weather`

There must be specific weather for this condition to return true. There are three possible options: sun, rain and storm. You need to specify `type:` argument followed by weather type.

**Example** `weather type:sun`

## Height: `height`

This condition requires player to be _below_ specific Y height. There is only one argument, `height:`, and it should be followed by an integer or double.

**Example** `height height:16`

## Armor Rating: `rating`

This one requires player to wear armor which gives him specified amount of protection (armor icons). There is only one argument, `rating:`, and it should be followed by an integer. One armor rating point is equal to half armor icon in-game (10 means half of the bar filled).

**Example** `rating rating:10`

## Random: `random`

This condition returns true randomly. There is one argument `random:` followed by two positive numbers `5-12`. They mean something like that: "It will be true 5 times out of 12".

**Example**: `random random:12-100`

## Sneaking: `sneak`

Sneak condition is only true when the player is sneaking. This would probably be useful for creating traps, I'm not sure. There are no arguments for this one.

**Example**: `sneak`
