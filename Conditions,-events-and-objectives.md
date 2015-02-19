# Conditions, events and objectives

## Conditions

Conditions are the most versatile and useful tools in creating advanced quests. They allow you to control what options are available to player in conversations, how the NPC responds or if the objective will be completed. The reference of all possible conditions is down below.

Creating conditions is simple. Open conditions.yml file. Now type a name for your condition in a new line, let's say `beton_started`. That could mean that you started quest beton (it's always better to call everything by what it does, so you don't get lost in a jungle of numeric meaningless references). Follow the name by colon and type instruction string (in single apostrophes, for safety). Instruction strings are pieces of text that define what type of condition is that and how it should work. Every condition in the reference has its own description of how to create instruction strings.

Let's say we want to check if player has `beton_start` tag (tags are little strings you can assign to player on certain events and then check if player has them). You would write instruction string like that: `tag tag:beton_start`. The first word is a condition type. It states that this should check for a tag (and not for eg. location). Second thing is `tag:beton_test`. This one defines what tag are we looking for. Note: you can't define more tags in one condition. For that you should create more conditions. Now if you use this condition in conversation option, it will make the option appear only, if the player has that tag. But what if you want the option to appear only if the player DOESN'T have that tag? In this case you should just prefix condition's name with `!`. _Note that it should be prefixed in conversation file, not in conditions.yml!_

Now you should have something like that: `beton_started: 'tag tag:beton_start'`

Using that you could check if player has already started this quest and deny him from starting it again. Of course the tag would be given upon starting the quest, by an event.

## Events

In certain moments you will want something to happen. Updating the journal, setting tags, giving rewards, all these are done using events. You define them just like conditions, by specifying a name and instruction string. You can find instruction strings to all events in the event reference. At the end of the instruction string you can add `event_conditions:` attribute followed by list of condition names separated by commas, like `conditions:angry,!quest_started`. This will make an event fire only when these conditions are met.

## Objectives

Objectives are the main things you will use when creating complex quests. You start them with a special event. At the end of the instruction string you can add conditions and events for the objective. Conditions will limit when the objective can be completed (e.g. killing zombies only at given location in quest for defending city gates), and events will fire when the objective is completed (e.g. giving a reward, or setting a tag which will enable collecting a reward from an NPC). You define these like that: "conditions:con1,con2 events:event1,event2" at the end of instruction string (note that it's different from "event_conditions:" which limits when the event will be fired). Separate them by commas, and never use spaces! Every objective needs additional `tag:` argument to name it for reference in objective cancel events.

**Example of a correct objective event**: `start_quest: 'objective mobkill ZOMBIE 10 conditions:night,!rain events:reward,add_tagjournal_entry tag:kill_zombies event_condition:!has_tag'`
