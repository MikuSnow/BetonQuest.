# Other important stuff

## Packages

All the content you create will be organized into packages. Each package contains the _main.yml_ file with package-specific settings, _conversations_ directory and all other files like _events.yml_ and _conditions.yml_. The default package is called simply "default". It is always present, and if you delete it, it will be regenerated with a sample quest.

If you want, you can simply ignore the existence of packages and write all your quests in the default one. You will however come to a point, when your files contain hundreds of lines and it gets a little bit confusing. That's why it's better to split your quests into multiple packages, for example "main" for the quests in the main city, "dungeon" for some interesting dungeon story etc.

Don't worry, you can reference things from other packages just by prefixing their names with packages. If you're writing a conversation in package `village` and you want to fire an event `reward` from package `beton`, you simply name the event as `beton.reward`. The plugin will search for `reward` in `beton` package instead of the one in which the conversation is defined. The same goes for "folder" event and "and"/"or" conditions.

There are however things you cannot reference from another packages - journal entries and quest items. For this you need to define an event/condition inside that package and reference this event.

## Variables

You can insert a variable in any instruction string. It looks like this: `$beton$` (and this one would be called "beton"). When the plugin loads that instruction string it will replace those variables with values assigned to them in _main.yml_ file. This will be useful for example when downloading a package from the internet containing a WorldEdit schematic of the quest building. Instead of going through the whole code to set those locations, names or texts you will only have to specify a few variables (that is, of course, only if the author of the package used those variables properly in the code).

There is a special type of variable - location modifiers. They follow a specific syntax, which looks like this: `$beton$->(12,0,-20)`. It means "take variable named _beton_ (which is a valid location, like that above) and add a vector (10,0,-10) to it". In the case below it would translate _derived_ variable to `112;200;280;world`, because **100 + 12 = 112**, zero does nothing and **300 + (-20) = 280**.

    variables:
      beton: 100;200;300;world
      derived: $beton$->(12,0,-20)

## Canceling quests

If you want to let your players cancel their quest there is a function for that. In _main.yml_ file there is `cancel` branch. You can specify there quests, which can be canceled, as well as actions that need to be done to actually cancel them. The arguments you can specify are:

* `name:` - this will be displayed to the player. All `_` characters will be converted to spaces. The only mandatory argument. If you want to translate the name to other languages, add additional `name_{lang}:` arguments, for example `name_pl:Nazwa_po_polsku`.
* `conditions:` - this is a list of conditions separated by commas. The player needs to meet all those conditions to be able to cancel this quest. Place there the ones which detect that the player has started the quest, but he has not finished it yet. 
* `objectives:` - list of all objectives used in this quest. They will be canceled without firing their events.
* `tags:` - this is a list of tags that will be deleted. Place here all tags that you use during the quest.
* `points:` - list of all categories that will be entirely deleted.
* `journal:` - these journal entries will be deleted when canceling the quest.
* `events:` - if you want to do something else when canceling the quest (like punishing the player), list the events here.
* `loc:` - this is a location to which the player will be teleported when canceling the quest (defined as in teleport event);

To cancel the quest you need to open your backpack and select a "cancel" button (by default a bone, can be changes by naming an item "cancel_button" inside default package). There will be a list of quests which can be canceled. Just select the one that interests you and it will be canceled.

## Global locations

Global locations are locations at which events can fire. They are defined as normal **location** objectives in events.yml and will fire when any player is in range of that location. Global locations are active for all players, even if they don't have an active objective. They can be used for starting location specific quest (such as encountering a dungeon and checking it out), teleporting players to arenas, this kind of stuff. They use tags to tell which player has been at certain location and which hasn't. These tags follow syntax `global_<tag>`, where `<tag>` is location objective's tag, defined at the end of instruction string (eg. `global_conversation_start`, where `conversation_start` is a tag of location objective). You can specify which events will be global locations in the _main.yml_ file inside a package, separating them with commas:

    global_locations: dungeon_entrance,trap,something_else

## Static events

Static events are events that will fire at the specified time of the day. They are not tied to a specific player, so not all of event types can be used as static. (Which player should receive a tag or objective? From which one should the items be taken?) Also, static events cannot have conditions defined (`event-conditions:` argument), as the plugin cannot check any condition without the player. Events, that can be used as static are flagges with `static` keyword in this documentation. You can define your static events in _main.yml_ file under `static` section, as such:

    static:
      '09:00': beton
      '23:59': lightning_strike
      '11:23': some_command

The hour must be in `''` to avoid problems, it needs leading zero if less than 10. `beton`, `lightnint_strike` etc. are IDs of events. There can only be one event specified, but it can be of type "folder".

## Journal

The journal is a book in which all your adventures are described. You can obtain it by typing **/j** command and selecting it from backpack. You cannot put it into chests, item frames and so on. If you ever feel the need to get rid of your journal, try to drop it - it will return to your backpack. The journal is updated with journal event, and the text inside is defined in _journal.yml_ config file. If you update these texts and reload the plugin, all players' journals will reflect changes. Colors of the journal can be altered in config.yml. The entries can use color codes, but the color will be lost between pages.

If you want to translate the entry do the same thing as with conversation option - go to new line, add language ID and the journal text for every language you want to include.

## Tags

Tags are little pieces of text you can assign to player and then check if he has them. They are particularly useful to determine if player has started or completed quest. For example you could give a player `quest_started` tag upon starting the quest, `quest_completed` when all objectives are done and finally `quest_payed` when NPC gives player his reward. Then you could create conditions named after these tags: `quest_started`, `quest_completed` and so on. Then you can create various conversation lines using these conditions: “(NPC) Do you want a quest?” if `!quest_started`, “(NPC) How is it going?” if `quest_started` and `!quest_payed`, “(player) I’ve done the quest!” if `quest_completed` and `!quest_payed` and so on. That was just an idea to get you started. You can do a lot more with these. Tags are package-neutral, meaning it doesn't matter from which package they are checked or started, they always look the same. You can however toggle the "tag_point_prefix" option in _main.yml_ file of every package. It will add prefixes with package name to all newly created tags and points. It will make the tags package-specific, but you will be unable to reference tags/points from other packages. This setting is good for packages that are self-contained.

## Points

Points are simply points. You can earn them for doing quest, talking with NPC’s, basically for everything you want. You can also take the points away, even to negative numbers. Points can be divided to categories, so the ones from _beton_ category won’t mix with points from _quests_ group. Of course then you can check if player has (or hasn’t) certain amount and do something based on this condition. They can be used as counter for specific number of quest done, as a reputation system in villages and even NPC’s attitude to player. Points also are package-neutral.

## NPCs

Conversations can be assigned to NPCs. You do it in the _main.yml_ file inside a package, in "npcs" section:

    npcs:
      '0': innkeeper
      'Innkeeper': innkeeper

The first string is the ID of the NPC, second is the corresponding conversation name. In case you use Citizens, ID is just the ID os an NPC. To acquire it just select the NPC and type `/npc`. If you don't want to use Citizens, you can also build NPCs as any other building in Minecraft:

Place somewhere a block of stained clay, no matter the color. Then place a head on top of it (type doesn't matter, it must be head). Now place a sign on the side of the clay block (it can be on it's back) and type in the first line `[NPC]`, and on the second line the ID of the NPC. You need to have permission `betonquest.createnpc` for that. Congratulations, you have created the NPC. Now you can add levers (hands) to it and maybe even fence gate (legs). Conversation is started by right clicking it's head.

## Items

If you want to use items in Give and Take events or Item and Hand conditions you must define them in items.yml file. This assures you that they will be exactly the same items. You can add them to this file in two ways:

1. Using the command `/q item <pack>.<itemID>`. It will take the item you are holding in hand and put it into items.yml inside <pack> package under `<itemID>` name. Easy and fast.

2. Manually. Add a new line to items.yml and type there item's ID followed by a colon and space. Now the first thing you need to do is insert item's type. You can find available types [here](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html). That's all you need for an item. Now there are some arguments you can add to make it better:
    * `data:` is the data value (eg. for different wool colors). It should be followed by an integer. Default value is 0, so in most cases you can omit it.
    * `name` is item's display name. All spaces should be replaced by `_`.
    * `lore:` is item's lore. Spaces follow the same rules as in name, and new lines are added by a semicolon.
    * `enchants:` is a list of enchants separated by command. Each enchantment has two values separated by a colon: name and level. All names can be found [here](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/enchantments/Enchantment.html). Example of two enchantments is `enchants:DAMAGE_ALL:3,KNOCKBACK:2`.
    * If the item is a written book you can also add `title:`, `author:` and `text:`. Spaces should be replaced by `_`, as always. The text can be divided to pages with `|` character and you can add new lines with `\n`.
    * If the item is a potion then you can add `effects:`, where all effects are separated by commas and are build like that: `EFFECT_NAME:X:Y` where list of available effect names is [here](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/potion/PotionEffectType.html), `X` is potion's power (1 is 1, not 2) and `Y` is duration in seconds (not ticks).
	* If the item is a leather armor part, you can specify color of it by adding `color:` with an integer. The integer can be easily generated with [this tool](http://www.shodor.org/stella2java/rgbint.html). If you need to get the color of a dye, just save a dyed armor to config via **/q item name** and see the exact result.
	* If the item is a player's head, you can specify it's owner by adding `owner:` followed by owner's name, for example `owner:Notch`.
	* If the item is an enchanted book just specify normal enchantments, they will be automatically applied to it as stored enchantments.

Sometimes you will want to target everything with your item, for example check if the player has any diamond sword (you don't want to let him go on a dangerous quest without proper equipment). Sometimes however you will want to target some specific simple item. Imagine a player has to bring a standard diamond sword to someone, so it can be enchanted with powerful magic. But he also carries his own, private _Diamond Sword of Beton and Destruction_. You don't want to take ANY diamond sword from him, as it could potentially remove his "private" sword. This is when "none" tag becomes useful.

If you want to target only item without any enchantments, or without a name (or potion without effects etc.), you should define it as `enchants:none` or `name:none` etc. The item will behave as usual, but targeting it with conditions and events will have special behavior.

Items cannot be translated, because it's not possible to track your every item and change it's metadata everytime you change the language. Sorry.

**Big note about books in 1.8 version of Minecraft**

It seems that some servers are adding `§0` at the end of every line when plugins generate books. It's usually no big deal, as this color code just resets the formating back to black color, but it can break item conditions (the item saved to configuration isn't the same as the one you've got with an event). Because of that I suggest you do the following to ensure that both books (the one in your hand and the other one in configuration) are identical:

1. Obtain a desired book (for example by writing it)
2. Save it with `/q item book` (or any other name, it doesn't matter for this example)
3. Get it by an event (`give book`)
4. Save the book you've just got again under the same name
5. Get the book again with the same event as before
6. That book will be identical as the one in configuration

I am very sorry for inconvenience, but removing those `§0`s automaticly could cause problems with formatting done by the user. I'm not going to risk that.

**Examples**:

    sword: 'DIAMOND_SWORD data:0 name:Slasher lore:Very_powerful;Forged_by_Endermen
      enchants:DAMAGE_ALL:5,KNOCKBACK:2'
    potion: 'POTION name:Poison lore:Will_kill_you_in_10_secods_flat effects:HARM:10:0'
    book: 'WRITTEN_BOOK title:Book_about_everything author:Notch
      text:The_text_goes_here.|This_is_on_the_new_page.\nAnd_this_is_one_line_below.'

_Note that YAML allows line breaking._

## Backpack

Sometimes you'll want some items to be persistent over death. If the player has lost them the quest would be broken. You can add a apecific line to item's lore to make it persistent (`&2Quest_Item` by default, `_` is a space in item's definition). Note that this must be a whole new line in the lore! Such item wouldn't be dropped on death, instead it would be placed in player's backpack. **Example**: `important_sword: 'DIAMOND_SWORD name:Sword_for_destroying__The_Concrete lore:Made_of_pure_Mithril;&2Quest_Item'`

To open your backpack just type **/j** command. The inventory window will open, displaying your stored items. The first slot is always the journal, and if you get it, the slot will stay empty. You can transfer quest items back and forth between inventories by clicking on them. Left click will transfer just one item, right click will try to transfer all items. Normal items cannot be stored into the backpack, so it's not an infinite inventory.

If you will ever have more than one page of quest items, the buttons will appear. You can customize those buttons by creating `previous_button` and `next_button` items in _items.yml_ file. Their name will be overwritten with the one defined in _messages.yml_.

Quest items cannot be dropped in any way other than using them. This way you can create a quest for eating cookies by giving the player a stack of cookies flagged as quest items and not continuing until there are no more cookies in his inventory/backpack. The player cannot drop the cookies, so he must eat every one of them to complete the quest.

Don't worry if the item-dropping filter isn't working for your items when you're in creative mode - it's not a bug. It's a feature. Creative-mode players should be able to easily put quest items in containers like TreasureChests.

## Party

Parties are very simple. So simple, that they don't even have to be created before using them. They are defined directly in conditions/events that use them. In such instruction strings the first argument is a number - range. It defines the radius where the party members will be looked for. Second is a list of conditions. Only the players that meet those conditions will be considered as members of the party. It's most intuitive for players, as they don't have to do anything to be in a party - no commands, no GUIs, just starting the same quest or having the same item - you choose what and when makes the party.

If you need an example of an instruction string of party condition/event, just look for `party` condition/event in condition/event list below.
