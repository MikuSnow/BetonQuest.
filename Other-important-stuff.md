# Other important stuff

## Global locations

Global locations are locations at which events can fire. They are defined as normal location objectives and will fire when the player is in range of that location. These objectives can be used for starting location specific quest (such as encountering a dungeon and checking it out), teleporting players to arenas, this kind of stuff. They use tags to tell which player has been at certain location and which hasn't. These tags follow syntax `global_<tag>`, where `<tag>` is location objective's tag, defined at the end of instruction string (eg. `global_conversation_start`, where `conversation_start` is a tag of location objective).

## Journal

The journal is a book in which all your adventures are described. You can obtain it by typing **/q journal** command. You cannot put it into chests, item frames and so on. If you ever feel the need to get rid of your journal, try to drop it, it will dissapear. The journal is updated with journal event, and the text inside is defined in _journal.yml_ config file.

## Tags

Tags are little pieces of text you can assign to player and then check if he has them. They are particularly useful to determine if player has started or completed quest. For example you could give a player `quest_started` tag upon starting the quest, `quest_completed` when all objectives are done and finally `quest_payed` when NPC gives player his reward. Then you could create conditions named after these tags: `quest_not_started`, `quest_started`, `quest_not_completed` and so on. These would use `--inverted` tag of course. Then you can create various conversation lines using these conditions: “(NPC) Do you want a quest” if `quest_not_started`, “(NPC) How is it going?” if `quest_started` and `quest_not_payed`, “(player) I’ve done the quest!” if `quest_completed` and `quest_not_payed` and so on. That was just an idea to get you started. You can do a lot more with these.

## Points

Points are simply points. You can earn them for doing quest, talking with NPC’s, basically for everything you want. You can also take the points away, even to negative numbers. Points can be divided to categories, so the ones from _beton_ category won’t mix with points from _quests_ group. Of course then you can check if player has (or hasn’t) certain amount and do something based on this condition. They can be used as counter for specific number of quest done, as a reputation system in villages and even NPC’s attitude to player.

## NPCs

There are to possibilities: you have Citizens plugin (1) or you don't have it (2).

1. When you’ll create your first conversation you will need to assign it to an NPC. To do so you must know NPC's ID (which you can find out by typing commands "/npc sel" and "/npc" when standing near the NPC. Now open _npcs.yml_ config file and add a new line `'X': conversation_name`. Upon reloading the plugin your NPC will have this conversation. No need for any traits.

2. You need to have permission `betonquest.createnpc`. Place somewhere a block of stained clay, no matter the color. Then place a head on top of it (type doesn't matter, it must be skull). Now place a sign on the side of the clay block (it can be on it's back) and type in the first line `[NPC]`, and on the second line the ID of the conversation (case sensitive!). You have created an NPC. Now you can add levers (hands) to it and maybe even fence gate (legs). Conversation is started by right clicking it's head.