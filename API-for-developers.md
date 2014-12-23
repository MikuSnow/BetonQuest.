API for developers
=============

Accessing the API
--------------------------

Just add BetonQuest.jar to your build path and you're good to go.

Writing events
--------------------

Writing events is the easiest. You need to create separate class extending pl.betoncraft.betonquest.core.QuestEvent for each new event. Then you must extract all information from instruction string which will be supplied at runtime. Don't worry about conditions, they are handled by the rest of BetonQuest's logic. When you'll finish your class you need to invoke registerEvents(String name, Class<? extends QuestEvent> class); from BetonQuest instance (which you can get using getInstance(); method). The string will be name for your event used in instruction strings (such as "journal" for journal event). The class argument is the Class object of your class. You can get it using YourObject.class. That's it, you created an event. Don't forget to check it for bugs.

Writing conditions
-------------------------

Writing conditions is more complicated. They must extend pl.betoncraft.betonquest.core.Condition and override isMet() method, which will return true or false depending on if condition was met. You register them using registerConditions(String name, Class<? extends Condition); method from BetonQuest instance as well. The rest is almost the same.

Writing objectives
--------------------------

Objectives are the most complicated because they use event handlers and must be persistent. They extend pl.betoncraft.betonquest.core.Objective. You also must override getInstructions(); method, which should return valid instruction string with updated informations (such as only 4 blocks left to pickup instead of initial 8) and unregister all listeners (this method is invoked only when an objective is saved or completed, thus listeners are not needed or could cause bugs). You can use tag, conditions and events fields from superclass for help (conditions and events are prefixed with "conditions:"/"events:" part, but the tag is not!).

Every accepted thing in your objective must be also verified with boolean checkConditions(); method. You don't want your objective ignoring all conditions, do you? When the objective is completed you should unregister all listeners and invoke completeObjective(); method. It will fire all events for you, so you don't have to do this manually.

Objectives are registered the same way as conditions and events, only using registerObjective(String name, Class<? extends Objective>); method.

Additional notes
------------------------

If you need to use player's ID (in code refered to as playerID) you should use PlayerConverter class and it's static methods. PlayerID is not a nick nor UUID. It is both at the same time, depending on how user will configure the plugin. That's why you can't use anything like Bukkit.getPlayer(playerID)

If you need to generate pages for a book from a single String please use JournalBook.pagesFromString(String string), which returns a List of string cut to proper length.
