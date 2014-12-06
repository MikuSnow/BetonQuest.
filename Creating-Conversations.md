# Creating conversations

Conversations are the base of your RPG system. It's the main method for starting and completing quests, as well as creating more immersive gameplay. You define every conversation in a separate file in "conversations" directory inside plugin'd root folder. This file's name should end with `.yml` extension, eq. `innkeeper.yml`.

Let’s start with picturing how it should look like at the end. Then we can try to understand how it’s done. From player's perspective conversation looks like this: player right-clicks on NPC (let's call them Innkeeper and Steve) (Steve is the player). Innkeeper says his initial text, and Steve can choose from let's say three options. He types in chat `1` (or `2` or `3`), and Innkeeper continues conversation saying something different. Steve again has options to choose and so on. If Steve types in chat some other things like letters of greater numbers, Innkeeper will respond that he doesn't understand him. Keeping this in mind let's write our first conversation.

Each conversation must define name of the NPC (some conversations are not bound to an NPC, so it’s important to specify it even though an NPC will have a name), his initial greeting options, his response to unknown player's answer and final events.

    quester: 'Innkeeper'
    unknown: 'I''m sorry, I didn''t understand. Can you repeat?'
    first: 'start,start_wood_started,start_wood_completed'
    final_events: ''
    stop: 'true'
    NPC_options:
      'start':
        text: 'Welcome to my inn %player%! What can I do for you?'
        conditions: 'wood_not_started'
        events: ''
        pointer: 'questions,quests,bye'
      'back':
        text: 'Yes?'
        conditions: ''
        events: ''
        pointer: 'questions,quests,wood_questions,wood_done,more_quests,bye'
    player_options:
      'questions':
        text: 'I have questions.'
        conditions: ''
        events: ''
        pointer: ''
      'back':
        text: 'Back to the topic...'
        conditions: ''
        events: ''
        pointer: 'back'

Note: Configuration files use yaml. Google it if you don't know anything about it. Main rule is that you must use two spaces instead of tabs. Another Note: That was just an example, it's part of default conversation included in the plugin.

`quester` is name of NPC. It should be the same as name of NPC this conversation is assigned to for greater immersion, but it's your call. `unknown` is what NPC will tell you when you select invalid option, and `first` are pointers to options John will use to welcome Steve. He will choose the first one that meets all conditions. You define these options in `npc_options` branch. `final_events` are events that will fire on conversation end, no matter how it ends (so you can create e.g. guards attacking the player if he tries to run). `stop` determines if player can move away from an NPC while in this conversation (false) or if he's stopped every time he tries to (true). Note two more spaces as we go deeper into hierarchy.

Now look at `start` option in npc branch. It has the same name as the initial pointer. `text` defines what will display on screen. `conditions` are names of conditions (more about them later) which must be met for this option to display, separated by commas. `events` is a list of events that will fire when an option is chosen (either by NPC or a player), defined similarly to conditions. `pointer` is list of pointers to the opposite branch (from NPC branch it will point to options player can choose from when answering, and from player branch it will point to different NPC reactions).

When an NPC wants to say something he will check conditions for the first option (in this case `wood_not_started`). If they are met, he will choose it. Otherwise, he will skip to next option (player has started the quest and NPC wants to comment it somehow). (Note: conversation ends when there are no options left). After choosing an option NPC will say it, and then the player will see options defined in `player_options` branch to which `start` points, in this case `questions`, `quests` and `bye`. If the conditions for a player option are not met, the option is simply not displayed, similar to texts from NPC. Player will choose option he wants, and it will point back to other NPC text, which points to next player options and so on.

If there are no possible options for player or NPC (either from not meeting any conditions or being not defined) the conversations ends. If the conversation ends unexpected check the console: It could be an error in configuration.

This can and will be a little confusing, so you should name your options, conditions and events in a way which you will understand in the future. Don't worry though, if you make some mistake in configuration, the plugin will tell you this in console when testing a conversation.