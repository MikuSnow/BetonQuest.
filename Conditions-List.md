Conditions List
==============

Item in Inventory
----------------

* **Name**: item
* **Desc**: This event is met only when player has defined item in his inventory.
* **Instruction**: There can be 2 attributes besides `--inverted`: `item:` is required, and represents an item defined in items.yml. `amount:` is amount of items the player must have (default is 1).
* **Example**: `item item:emerald amount:1 --inverted`

Item in Hand
----------------

* **Name**: hand
* **Desc**: This event is met only when player is holding a specific item in his hand. Amount doesn’t matter, though it may be checked with Item in Inventory condition.
* **Instruction**: Just like the above but without `amount:` attribute.
* **Example**: `hand item:sword`

Alternative
----------------

* **Name**: or
* **Desc**: Alternative of specified conditions. This means that only one of conditions has to be met in order for alternative to be true.
* **Instruction**: You just define one argument, `conditions:` followed by condition names separated by commas. `--inverted` argument works as always.
* **Example**: `or conditions:night,rain,has_armor`

Conjunction
----------------

* **Name**: and
* **Desc**: Conjunction of specified conditions. This means that every condition has to be met in order for conjunction to be true. Used only in complex alternatives, as conditions normally work as conjunction.
* **Instruction**: Exactly the same as alternative.
* **Example**: `and conditions:has_helmet,has_chestplate,has_leggings,has_boots`

Location
-------------

* **Name**: location
* **Desc**: It returns true only when player is closer to specified location than given distance.
* **Instruction**: Just one attribute, specified as `loc:` and location defined exactly as in location objective.
* **Example**: `location loc:100;200;300;world;5 --inverted`

Health
-----------------

* **Name**: health
* **Desc**: Requires player to have equal or more (or less using `--inverted`) health than specified amount.
* **Instruction**: Only one attribute, `health:` followed by a number (double). Players can have 0 to 20 health by default (there are some mods which change that).
* **Example**: `health --inverted health:5.6`

Experience
-----------------

* **Name**: experience
* **Desc**: This condition is met when player has specified level (default minecraft experience). It is measured by full levels, not experience points.
* **Instruction**: The instruction string must contain argument `exp:X` where X is integer, eg. `exp:20`. If you add `--inverted` argument then outcome will be negated.
* **Example**: `experience exp:30`

Permission
-----------------

* **Name**: permission
* **Desc**: Player must have certain permission for this condition to return true.
* **Instruction**: The instruction string must contain argument `perm:permission.node`. `--inverted` argument negates outcome.
* **Example**: `permission --inverted perm:essentials.tpa`

Point
-----------------

* **Name**: point
* **Desc**: Requires player to have equal or more (or less with `--inverted`) points from category than specified.
* **Instruction**: There are two arguments, `category:` followed by a string and `count:` followed by an integer.
* **Example**: `point category:beton count:20 --inverted`

Tag
----------------

* **Name**: tag
* **Desc**: This one requires player to have a tag set by tag event. Together with `--inverted` negation it is one of the most powerful tools whencreating conversations.
* **Instruction**: The instruction string must contain `tag:some_text` argument, where some_text it's tag string. As usual the `--inverted` attribute negates outcome.
* **Example**: `tag tag:quest_completed`

Armor
----------------

* **Name**: armor
* **Desc**: The armor condition requires player to wear given armor type, optionally with enchantments of equal or greater power than specified.
* **Instruction**: There can be 3 arguments: `type:` is type of armor (possible options are helmet, chestplate, leggings and boots), `material:` is the material of armor (possible options are leather, gold, chainmail, iron and diamond) and `enchants:` is a list of enchantments defined exactly as in item condition.
* **Example**: `armor type:helmet material:iron enchants:PROTECTION_ENVIRONMENTAL:2,THORNS:1`

Potion Effect
----------------

* **Name**: effect
* **Desc**: To meet this condition player must be under specified potion effect.
* **Instruction**: There is only one argument, `type:`, and it takes values from this page: [potion types](http://jd.bukkit.org/rb/apidocs/org/bukkit/entity/EntityType.html)
* **Example**: `effect type:SPEED --inverted`

Time
----------------

* **Name**: time
* **Desc**: There must be specific time for this condition to return true.
* **Instruction**: You need to specify `time:` attribute followed by two hour numbers separated by dash. These number are normal 24-hour format hours. The first must be smaller than the second. If you want to achieve time period between 23 and 2 you need to invert outcome.
* **Example**: `time time:2-23 --inverted`

Weather
----------------

* **Name**: weather
* **Desc**: There must be specific weather for this condition to return true. There are three possible options: sun, rain and storm.
* **Instruction**: You need to specify `type:` argument followed by weather type.
* **Example**: `weather type:sun`

Height
----------------

* **Name**: height
* **Desc**: This condition requires player to be below specific Y height.
* **Instruction**: There is only one argument, `height:`, and it should be followed by an integer or double.
* **Example**: `height height:16`
