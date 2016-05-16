![BetonQuest](http://betonquest.betoncraft.pl/logo.png)

**Documentation for 1.8 versions**

BetonQuest is advanced and powerful quests plugin. It offers RPG-style conversations with NPCs and a very flexible quest system. Instead of being limited to creating "quest" objects with take requirements and completion rewards, BetonQuest allows you to freely define what should happen (events), if it should happen (conditions) and what needs to be done for it to happen (objectives). Your quests don't have to look like "kill, bring, get reward": you can create multi-threaded stories, narrated with NPC conversations, with multiple endings affecting the player's gameplay in many ways.

## Features

* **Much more than just a questing plugin**
* **Powerful event system**: anything you want can happen anywhere in a quest
* Even more **powerful condition system**: you can limit whenever something should (or shouldn't) happen
* **Multiple choice conversations** with NPCs optionally using an inventory GUI
* **Party system** allowing for creation of group quests
* **Journal** in a book
* **Backpack** for quest items
* Advanced item handling which considers even text in books
* Ability to create various **reputation systems** (points)
* Firing events for a players when they enter specified area (global locations)
* **Daily quests** or repeatable reward collection (`delay` objective)
* Variables in conversations - let the NPC tell how much more wood he needs!
* Quests can be organized into distributable packages
* **Citizens2** NPC support
* Integrated with MythicMobs, mcMMO, Heroes, SkillAPI, Quests, Skript, Denizen, Magic, WorldGuard, Vault, EffectLib and PlayerPoints
* Multiple languages and easy translating
* API for creating your own events, conditions and objectives
* SQLite and **MySQL** support
* Last but not least, an **active, open source** project with development builds available

## Overview

Let me show you a little example to better understand what BetonQuest allows you to do as a quest writer.

Imagine you have a conversation with an NPC. You can choose from multiple options, and the NPC will react differently, for example he will tell you to cut some trees when asked for a job. If you tell him that you accept his offer, an event will be fired. It will start an objective for getting wood. It will also "tag" you as someone who started the quest. From now on the NPC will check for that tag, and use different options in the conversation, for example telling you to hurry up.

When you complete the objective (by breaking wood blocks), the objective will fire another event. This one will "tag" you as someone who collected the wood. When you go back to the NPC and tell him about it, he will check (using a condition) if you actually have the wood in your inventory. If so, he will fire another event, giving you the reward.

There was no single "quest" object. This was only a conversation, which was firing events and checking conditions. The objective also wasn't a "quest" - it only added a tag when you collected the wood, nothing more. It could not exist on it's own. The same conversation on the other hand could start some other quests afterwards (for example mining some ore), so it's also not a "quest". This is the main source of BetonQuest's strength - instead of trying to force you into a hardcoded pattern, it gives you tools to create your own patterns. It is more difficult to write quests that way, but the results are worth it.

Don't be disappointed by my examples of getting wood and mining ore. These were only simplifications, so it's easier to explain the system. BetonQuest is capable of much more. You can add entries to player's journal based on the quests he's doing like in Morrowind, the conversations can be as multi-threaded as in Baldur's Gate and quests can be started by entering specific location like in Skyrim. You can create reputation systems, unique quest items, books that react to reading them and so on. Your quests can have multiple ways to different endings depending on players' decisions and they can require multiple players to do something.

You don't have to use BetonQuest for quests only. Conversations with NPCs can help your players, teleports them around the map, describe server features, buy or sell stuff, give ranks etc. The only limit is your imagination!
