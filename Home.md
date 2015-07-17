![BetonQuest](http://betonquest.betoncraft.pl/logo.png)

**Documentation for 1.7 version**

BetonQuest is advanced and powerful quests plugin. It doesn't follow traditional convention, where a "quest" is a closed structure object. Instead, BetonQuest introduces a network of objectives which can under certain conditions trigger events. Your quests don't have to look like "kill, bring, get reward": you can create multi-threaded quests, narrated with NPC conversations, with multiple endings affecting player's gameplay in many ways.

## Features

* Adventures you create are not limited to boundaries of a "quest" object
* Powerful event system: anything you want can happen anywhere in a quest
* Powerful conditions system: you can limit whenever something should (or not) happen
* Party system allowing for creation of group quests
* Multiple choice conversations with NPCs
* Journal in a book
* Backpack for quest items
* Advanced item handling which considers even text in books
* Tags for storing player's progress and other information
* Various reputation systems using Points
* Global locations: firing events for a players when they enter specified area
* Delay for events - daily quests or repeatable reward collection
* Quests can be organized into distributable packages
* Citizens2 NPC support
* MythicMobs, Skript, WorldGuard and Vault integration
* Multiple languages and easy translating
* Players can choose their own language
* API for creating your own events, conditions and objectives
* SQLite and MySQL support
* Configuration and database backups
* Automatic updater 

## Overview

So how does this work exactly? I'll describe it with a simple example of the quest for getting wood. Note the difference between "events", "conditions" and "objectives".

Firstly, you create a conversation with the NPC. The player can choose from multiple options in this conversation, and the NPC will react differently (for example he will tell the player to cut some trees when asked for a job). In some place there will be an event fired, which will add an objective for getting wood, and it will tag the player as someone who started the quest. From now on the NPC will use different options in the conversation, for example telling the player to hurry up. These options will be chosen based on conditions.

When the player completes the objective (for example by breaking the wood), the event will fire tagging him as someone who collected the wood. When he goes back to the NPC and tell him about getting the wood, NPC will check using conditions if the player actually has the wood. If so, he will fire the event giving a reward.

We did not create any "quest" object. This was only a conversation, which fired events and checked conditions. The objective also wasn't a "quest" - it only tagged the player when he collected the wood, it could not exist on it's own. The conversation on the other hand could start some other quest afterwards (for example mining some ore), so it's also not a "quest".

Don't be disappointed by my examples of getting wood or mining ore. These were only simplifications, so it's easier to explain the system. BetonQuest is capable of much more. The conversations can be as multi-threaded as in Baldur's Gate or Skyrim, the quests can have multiple ways to the ending, and there can be multiple different endings, which can affect reputation of the player etc. It's up to you.

The plugin also features an in-book journal. Have you ever played Morrowind? It's almost the same, we just reversed the order in which you see entries, so you don't have to click through hundreds of pages. Now quests don't need to display messages like "You collected every ore, now return to Miner". Instead they can update player's journal with new entry "I collected every single ore. I should return to Miner and get my reward!" That's way more immersive.
