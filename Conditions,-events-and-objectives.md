# Conditions, events and objectives

Conditions, events and objectives are defined with an "instruction string". It's a piece of text, formatted in a specific way, containing the instruction for the condition/event/objective. Thanks to this string they know what should they do. To define the instruction string you will need a reference, few pages below. It describes how something behaves and how it should be created. All instruction strings are defined in appropriate files, for example all conditions are in _conditions.yml_ config. The syntax used to define them looks like this: `name: 'the instruction string containing the data'`. Apostrophes are optional in most cases, you can find out when by looking up "YAML" in Google. I will describe instruction strings in a more detailed way using conditions:

## Conditions

Conditions are the most versatile and useful tools in creating advanced quests. They allow you to control what options are available to player in conversations, how the NPC responds or if the objective will be completed. The reference of all possible conditions is down below.

Let's say we want to check if player has `beton_start` tag (tags are little strings you can assign to player on certain events and then check if player has them). You would write instruction string like that: `tag beton_start`. The first word is a condition type. It states that this should check for a tag (and not for eg. location). Second thing is `beton_test`. This one defines what tag are we looking for. _Note: you can't define more tags in one condition. For that you should create more conditions._ Now if you use this condition in conversation option, it will make the option appear only if the player has that tag. But what if you want the option to appear only if the player DOESN'T have that tag? In this case you should just prefix condition's name with `!`. _Note that it should be prefixed in conversation file, not in conditions.yml!_

Now you should have something like that: `beton_started: 'tag beton_start'`

Using that you could check if player has already started this quest and deny him from starting it again. Of course the tag would be given upon starting the quest, by an event:

## Events

In certain moments you will want something to happen. Updating the journal, setting tags, giving rewards, all these are done using events. You define them just like conditions, by specifying a name and instruction string. You can find instruction strings to all events in the event reference. At the end of the instruction string you can add `conditions:` attribute followed by list of condition names separated by commas, like `conditions:angry,!quest_started`. This will make an event fire only when these conditions are met.

## Objectives

Objectives are the main things you will use when creating complex quests. You start them with a special event, `objective`. You define them in the _objectives.yml_ file, just as you would conditions or events. At the end of the instruction string you can add conditions and events for the objective. Conditions will limit when the objective can be completed (e.g. killing zombies only at given location in quest for defending city gates), and events will fire when the objective is completed (e.g. giving a reward, or setting a tag which will enable collecting a reward from an NPC). You define these like that: "conditions:con1,con2 events:event1,event2" at the end of instruction string . Separate them by commas and never use spaces!

Objectives are loaded at start-up, but they do not consume resources without player actually having them active. This means that if you have 100 objectives defined, and 20 players doing one objective, 20 another players doing second objective, and the rest objectives are free (no one does them), then only 2 objectives will be active, not 100, not 40. That makes it more efficient.

**Example of a correct objective event**: `quest: 'mobkill ZOMBIE 10 conditions:night,!rain events:reward,add_tag,journal_entry'`
