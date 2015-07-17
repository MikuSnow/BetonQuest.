# Info for developers

## Accessing the plugin

Just add BetonQuest.jar to your build path and you're good to go.

## Writing events

Writing events is the easiest. You need to create a class extending `pl.betoncraft.betonquest.api.QuestEvent` for each new event. In the constructor you must extract all information from instruction string which will be supplied at runtime. The constructor must take two string arguments: package name and the instruction. Don't worry about conditions, they are handled by the rest of BetonQuest's logic. Event is not bound to any player, and firing it is done through `fire(String playerID)` method. You have to override it with the code responsible for firing the event using the data extracted by the constructor. When you'll finish your class you need to invoke `registerEvents(String name, Class<? extends QuestEvent> class)` from BetonQuest instance (which you can get using `getInstance()` static method). The name for your event will be used in instruction strings (such as "journal" for journal event). The class argument is the Class object of your event. You can get it using `YourEvent.class`. That's it, you created an event. Don't forget to check it for bugs.

## Writing conditions

Writing conditions is more complicated. They must extend `pl.betoncraft.betonquest.api.Condition` and override `check(String playerID)` method, which will return true or false depending on if condition was met. You register them using `registerConditions(String name, Class<? extends Condition)` method from BetonQuest instance as well. The rest is almost the same, you're defining the constructor which will parse the instruction string and overriding `check(String playerID)` method to check if the player meets the condition. Don't worry about inverting it, as it's automatically done in `isMet(String playerID)` method.

## Writing objectives

Objectives are the most complicated because they use event handlers and they must store players' data. They extend `pl.betoncraft.betonquest.api.Objective` class. As always, you need to extract all data from supplied instruction string in the constructor. The constructor takes additional argument, label of the objective (the key from _objectives.yml_), between package name and instruction. Don't register listeners in the constructor, that's what `start()` method is for.

If your objective handles changing data you should create a class extending `ObjectiveData`.  For example `block` objective does need to store amount of blocks left to place/break, and it does that using "BlockData" class. In the constructor it receives three strings: data string, ID of the player and ID of the objective. You define yourself how the data string should look like, how it should be parsed and the methods to alter the data from the objective. You also need to override the `toString()` method in so it returns data string in the format parsable by your constructor. Everytime the data in your object changes, you need to call `update()` method. It will save the data to the database.

Now you should override `getDefaultDataInstruction()` method. It must return the default data instruction understandable by this objective's data object. For example `tame` objective will return here the amount of mobs to tame. If you don't use data objects, just return an empty string (not `null`, just "").

In order for your objective to use the data object you have created you need to set the `template` variable to this object's class. If you're not defining the data object (because you don't need to handle the changing data), you should set the `template` simply to `ObjectiveData.class`.

Every time your objective accepts the player's action (for example killing the right mob in MobKill objective) it must be also verified with `checkConditions()` method. You don't want your objective ignoring all conditions, right? When the objective is completed you should call `completeObjective()` method. It will fire all events for you, so you don't have to do this manually. It will also call `stop()` method, which will unregister all listeners, so don't do that manually.

`start()` and `stop()` methods must start objective's listeners and stop them accordingly. It's because the plugin turns the objective off if there are no players having it active. Normally you will register/unregister listeners here, but some objectives may be different. For example `delay` objective starts a repeating runnable and cancels it.

Objectives are registered the same way as conditions and events, using `registerObjective(String name, Class<? extends Objective>)` method.

## Firing events

The plugin class (BetonQuest) has static method for firing events - `event(String playerID, String eventID)`. First parameter is ID of the player. Second one represents ID of the event, which consists of the package name and it's name from "events.yml", separated by a dot (for example `default.wood_reward`). Currently you can't fire an event directly using an instruction string.

## Checking conditions

BetonQuest has static boolean method `condition(String playerID, String conditionID)`. It works similarly as event method described above.

## Starting objectives

Normally if you want to start the objective you should use `newObjective(String playerID, String objectiveID). It will just add this objective to the player as the `objective` event would do. You can however use `resumeObjective(String playerID, String objectiveID, String instruction)`, which will use the supplied data instruction to start the objective. It will not save it to the database, because it is assumed that the objective has just been loaded from it and it exists there without any change.

## Creating additional conversation input/output methods

In order to register an object as the conversation input/output it needs to implement `ConversationIO` interface. The constructor will receive three arguments: Conversation object, playerID String and NPC name String. It needs to parse the required data here and register all needed listeners. The `setResponse(String response)` method will receive NPC's text from the conversation. The `addOption(String option)` method will be called by the conversation for each reply option for this NPC text. The object must store all this data and when `display()` is called, it must use it to display the player the output. When it detects that the player chose an answer, it should pass it to the conversation using `Conversation.passPlayerAnswer(int number)` method. The integer is the number of the answer, starting at 1. `clear()` method will be called at the beginning of the new conversation cycle. It should clear all the previous options, so they do not overlap. `end()` method will be called when the conversation ends and it should unregister all listeners. You can also call that message when you detect that the player forced conversation ending (for example by moving away from the NPC). Remember to notify the conversation about that using `Conversation.end()`.

Registering the conversation inputs/outputs is done in the same way as objectives, events and conditions, through `BetonQuest.registerConversationIO(String name, Class<? extends ConversationIO>)` method.

## Debug

You can debug your code using Debug class.
