![Logo](http://i.imgur.com/Gy9ORlk.png)

BetonQuest is advanced and powerful quests plugin. It doesn't follow traditional convention, where "quest" is a closed structure object, which can have a set of tasks, events and rewards on completion. Instead, BetonQuest introduces the net of objectives which can under certain conditions trigger events, start new objectives or change NPC's attitude to the player. Of course grouping this all together and saying "this group is a quest" is still possible.

## Features

* Adventures you create are not limited to boundaries of a "quest"
* Powerful event system: anything you want can happen anywhere in a quest
* Powerful conditions system: you can limit whenever something should (or not) happen
* Multiple choice conversations with NPCs
* No immersion breaking interface elements
* Journal in a book
* Item checks are considering everything, even text in books
* Tags for storing player's progress and other information
* Various reputation systems using Points
* Global locations: firing events for a player when he enters specified area (without active objective)
* Delay for events - daily quests or repeatable reward collection
* Citizens2 NPC support
* UUID or names
* Multiple languages and easy translating
* API for creating your own events, conditions and objectives
* SQLite and MySQL support
* Automatic updater 

## Description

So how does it work? Let's show you a simple example of a quest for getting wood. You create a conversation which at some point fires an event adding an objective for the player. Now the NPC can react differently to the player in conversations (eg. comment player's progress or tell him to hurry up). It's done with conditions, every line in conversation can has then and appear only when they are met. As the player finished his objective you tag him (using an event) with proper message, and NPC will check (using a condition) if the player has this tag. If he does then an event giving a reward will be fired. Note that you haven't defined a single "quest" object. You've just connected a set of objectives, events, conditions and conversations together and said "this is a quest". That's the power of BetonQuest: you are not limited by pointless boundaries of a "quest". If you want you can even create a network so big and complicated that it will be impossible to say where a quest starts and where it ends. It's up to you.

Advanced conditioning allows you to create even more complicated quests. Requiring player to be dressed in red leather armor, holding rotten flesh in hand, in the middle of night in order to summon some demons (just an example) is not a problem. Furthermore, you can group your conditions in logic sentences, use conjunction and alternative on them, and of course negation.

BetonQuest is highly integrated with Citizens' NPCs. It uses them to deliver RPG style conversations. You don't just start a quest clicking on the NPC: you can talk with them by selecting options, just like in Baldur's Gate or Skyrim. These options can also appear only under specific conditions, so it's not a problem to create dynamic conversations.

The plugin also features an in-book journal. Have you ever played Morrowind? It's almost the same, we just reversed the order in which you see entries, so you don't have to click through hundreds of pages. Now quests don't need to display messages like "You collected every ore, now return to Miner". Instead they can update player's journal with new entry "I collected every single ore. I should return to Miner and get my reward!" That's waaay more immersive.

BetonQuest has a simple API for adding new types of objectives, conditions and events. You can make a score condition for your PvP plugin, or even objective of killing some amount of players (I don't like PvP, so I won't include this in the plugin by myself).

## Notes

_As of 1.2 BetonQuest uses Metrics system to send anonymous data to [McStats.org](http://mcstats.org/plugin/BetonQuest). You can disable it by setting "metrics" to false in configuration file._

_As of 1.4 BetonQuest features auto-updater. In 1.4 it's disabled by default. In 1.5 it's enabled by default. You can enable/disable this by setting "autoupdate" to true/false in configuration file. It's 100% safe, as all downloaded updates will be approved by Bukkit staff. Additionally the plugin will backup all your data before each update and create changelog file just for you. You will also receive a notification about the update when you join the server._

_Development builds of BetonQuest can be acquired [here](http://betoncraft.pl/downloads). These builds may contain a lot of bugs. **Use them at your own risk!**_
