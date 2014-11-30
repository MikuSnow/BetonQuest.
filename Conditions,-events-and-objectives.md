# Conditions, events and objectives

## Conditions

Conditions are the most versatile and useful tools in creating advanced quests. They allow you to control what options are available to player in conversations, how the NPC responds or if the objective will be completed. The reference of all possible conditions is down below.

Creating conditions is simple. Open conditions.yml file. Now type a name for your condition in a new line, let's say `beton_started`. That could mean that you started quest beton (it's always better to call everything by what it does, so you don't get lost in a jungle or numeric meaningless references). Follow the name by colon and type instruction string (in single apostrophes, for safety). Instruction strings are pieces of text that define what type of condition is that and how it should work. Every condition in the reference has its own description of how to create instruction strings.

Let's say we want to check if player DOESN'T have `beton_start` tag (tags are little strings you can assign to player on certain events and then check if player has them). You would write instruction string like that: `tag --inverted tag:beton_start`. The first word is condition type. It states that this should check for a tag (and not for e.g. location). Second is `--inverted` argument, which negates the output. In this case condition will be met if the player DOESN'T have this tag. Last thing is `tag:beton_test`. This one defines what tag are we looking for. Note: you can't define more tags in one condition. For that you should create more conditions.

Now you should have something like that: `beton_started: 'tag --inverted tag:beton_start'`

Using that you could check if player has already started this quest and deny him from starting it again. Of course the tag would be given upon starting the quest, by an event.

**List of all available condition can be found here: [Conditions List]()**

## Events

In certain moments you will want something to happen. Updating the journal, setting tags, giving rewards, all these are done using events. You define events just like conditions, by defining a name and instruction string. You can find instruction strings to all events in the event reference. At the end of the instruction string you can add `conditions:` attribute followed by list of condition names separated by commas, like `conditions:angry,quest_not_started`. This will make an event fire only when these conditions are met.

**List of all available events can be found here: [Events List]()**

## Objectives

Objectives are the main things you will use when creating complex quests. Defining one is almost exactly the same as events and conditions. The only difference is that at the end of the instruction string you add conditions and events. Conditions will limit when the objective can be completed (e.g. killing zombies only at given location in quest for defending city gates), and events will fire when the objective is completed (e.g. giving a reward, or setting a tag which will enable collecting reward from an NPC). You define these like that: "conditions:con1,con2 events:event1,event2" at the end of instruction string. Separate them by commas, and never use spaces (except between conditions and events of course). Every objective needs additional `tag:` argument to name it for reference in objective cancel events.

Objectives are started by a special objective event.

**List of available objectives can be found here: [Objectives List]()**