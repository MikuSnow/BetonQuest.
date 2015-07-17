# Creating conversations

Conversations are the base of your RPG system. It's the main method for starting and completing quests, as well as creating more immersive gameplay. You define every conversation in a separate file in "conversations" directory inside a package (more about packages later, for now just look into "default" folder inside BetonQuest directory). This file's name should end with `.yml` extension, eg. `innkeeper.yml`.

Let’s start with picturing how it should look like at the end. Then we can try to understand how it’s done. From player's perspective conversation looks like this: player right-clicks on NPC (let's call them Innkeeper and Steve) (Steve is the player). Innkeeper says his initial text, and Steve can choose from, let's say three options. He types in chat `1` (or `2` or `3`), and Innkeeper continues conversation saying something different. Steve again has options to choose and so on. If Steve types in chat some other things like letters of greater numbers, Innkeeper will respond that he doesn't understand him. Keeping this in mind let's write our first conversation.

Each conversation must define name of the NPC (some conversations can be not bound to any NPC, so it’s important to specify it even though an NPC will have a name), his initial greeting options, his response to unknown player's answer and final events.

    quester: Innkeeper
    unknown: 'I''m sorry, I didn''t understand. Could you repeat?'
    first: start,start_wood_started,start_wood_completed
    final_events: give_emeralds,remove_points
    stop: 'true'
    NPC_options:
      start:
        text: Welcome to my inn %player%! What can I do for you?
        conditions: wood_not_started
        events: example_event
        pointer: questions,quests,bye
      back:
        text: Yes?
        events: set_tag,journal_entry
        pointer: questions,quests,wood_questions,wood_done,more_quests,bye
    player_options:
      questions:
        text: I have questions.
        conditions: has_points,has_emeralds
        pointer: answer
      bye:
        text: I must go.

Note 1: _Configuration files use yaml. Google it if you don't know anything about it. Main rule is that you must use two spaces instead of tabs when going deeper into the hierarchy tree. If you want to write `'` character, you must double it and surround the whole text with another `'` characters (for example `unknown` option above). When writing `true` or `false` it also needs to be surrounded with `'`. If you want to start the line with `&` character, the whole line needs to be surrounded with `'`._

Note 2: _That conversation was just an example. It isn't valid, because it's missing a lot of other options._

`quester` is name of NPC. It should be the same as name of NPC this conversation is assigned to for greater immersion, but it's your call. `unknown` is what NPC will tell you when you select invalid option, and `first` are pointers to options John will use to welcome Steve. He will choose the first one that meets all conditions. You define these options in `npc_options` branch. `final_events` are events that will fire on conversation end, no matter how it ends (so you can create e.g. guards attacking the player if he tries to run). You can leave this option out if you don't need any final events. `stop` determines if player can move away from an NPC while in this conversation (false) or if he's stopped every time he tries to (true). If enabled, it will also suspend the conversation when the player quits, and resume it after he joins back in. This way he will have to finish his conversation no matter what. _It needs to be in `''`!_ Also note two more spaces as it goes deeper into the hierarchy tree.

Now look at `start` option in npc branch. It has the same name as the initial pointer. `text` defines what will display on screen. `conditions` are names of conditions (more about them later) which must be met for this option to display, separated by commas. `events` is a list of events that will fire when an option is chosen (either by NPC or a player), defined similarly to conditions. `pointer` is list of pointers to the opposite branch (from NPC branch it will point to options player can choose from when answering, and from player branch it will point to different NPC reactions). If you don't want to set any events/conditions/pointers to the option, just skip them. Only `text` is always required.

When an NPC wants to say something he will check conditions for the first option (in this case `wood_not_started`). If they are met, he will choose it. Otherwise, he will skip to next option (player has started the quest and NPC wants to comment it somehow). (Note: conversation ends when there are no options left). After choosing an option NPC will say it, and then the player will see options defined in `player_options` branch to which `start` points, in this case `questions`, `quests` and `bye`. If the conditions for a player option are not met, the option is simply not displayed, similar to texts from NPC. Player will choose option he wants, and it will point back to other NPC text, which points to next player options and so on.

If there are no possible options for player or NPC (either from not meeting any conditions or being not defined) the conversations ends. If the conversation ends unexpected check the console: It could be an error in configuration.

While the player has a conversation with an NPC, his normal chat messages are interpreted as replies in the conversation. But if he needs to send something to the global chat he can prefix his message with `#` character. The message will be handled as a normal chat message.

This can and will be a little confusing, so you should name your options, conditions and events in a way which you will understand in the future. Don't worry though, if you make some mistake in configuration, the plugin will tell you this in console when testing a conversation. Also, study the default conversation included with the plugin to fully understand how powerful this system can be.

## Translations

As you can see in default conversation, there are additional messages in other languages. That's because you can translate your conversations into multiple languages. The players will be albe to choose their preferred one with **/questlang** command. You can translate every NPC/player option, quester's name and "unknown" message. You do this like this:

    quester:
      en: Innkeeper
      pl: Karczmarz
      de: Gastwirt

As said before, the same rule applies to all options and the "unknown" message. The player can choose only from languages present in _messages.yml_, and if there will be no translation to this language in the conversation, the plugin will fall back to the default language, as defined in _config.yml_. If that one is not defined, there will be an error.

You can also translate journal entries, quest cancelers and `message` events, more about that later.
