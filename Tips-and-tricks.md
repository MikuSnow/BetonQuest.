# Tips and tricks

## Handling death in your quests

Sometimes, while writing a dangerous quest you will want something specific to happen when the player dies. If it's a boss battle you may want to fail the quest, if it's a dungeon you may want to respawn the player at the beginning of a level etc. You can do that with `die` objective - simply start it for the player at the beginning of the quest and make it fire events that will do the thing you want (like teleporting the player to desired respawn point, removing tags set during the quest etc).

## Creating regions for one player at the time

Imagine you have a room to which the player is teleported. Then suddenly mobs start to spawn and the player must kill them (because it's a trap or something). The player has killed all the mobs, he got a tag and wants to proceed but all of the sudden another player teleports into the room and all the mobs start to spawn again. The first player is quickly killed and the second one easily kills all mobs. You can prevent such situations by using `party` condition. Just check with it if the party consisting of "players inside the room" has greater amount of players that 1. Set the range to something big enough so it covers the room and the party condition can be tag or location.

## Racing with folder event

Since `folder` event can run `tag` events even for offline players you can create races. Create `location` objective where you want the finish line to be and condition it with negated "race_failed" tag (or similar). It will mean that "if the player has not failed the race, he can win it by reaching the location". Now when the race starts fire `folder` event with the amount of time you want to give your players to complete the race. This event should set "race_failed" tag. If the player reaches the location before this tag is set, he will fire all events in that `location` objective, but if the time has passed, the objective will not be completed. You can figure the rest out for yourself.

## Random daily quests

Starting the random quest must be blocked with a special tag. If there is no such tag, the conversation option should appear. Create a few quests, each of them started with single `folder` event (they **must** be started by single event!). Now add those events to another `folder` event and make it `random:1`. At the end of every quest add `delay` which will reset the special blocking tag. Now add that `folder` event to the conversation option. When the player chooses it he will start one random quest, and the conversation option will become available after defined in `delay` objective time after completing the quest.

## Each day different quest (same for every player)

To do this use something called "[Static event](https://github.com/Co0sh/BetonQuest/wiki/Other-important-stuff#static-events)". Using the static event run `folder` event every day at some late hour (for example 4am). The `folder` event should be `random:1` and contain several different `setblock` events. These events will set some specific block to several different material types (for example dirt, stone, wood, sand etc). Now when the player starts the conversation and asks about the daily quest the NPC should check (using `testforblock` condition) which type of block is currently set and give the player different quest, depending on the block type.
