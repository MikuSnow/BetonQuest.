# TODO List

The changes marked as done will appear in the next version. The ones on top describe what I am working on and the rest needs to be done.

* [ ] Denizen support (mainly for firing events but I'll try to add checking conditions in scripts (useful for points and tags))
* [X] MythicMobs support (and mob name support in MobKill objective, why not?)
* [X] Creating objectives directly from event, without referencing the objectives.yml file (it is unneeded complication as there can always be exactly one event for every objective)
* [X] Modify command event to accept multiple commands
* [X] Add support for new lines in books (journal.yml, items.yml)
* [X] Add several aliases for commands, it looks like /q and /j are popular among other developers...
* [ ] Permission for conversation starting
* [ ] Sounds for journal and conversations
* [ ] Clickable answers in chat (with tellraw) using commands to prevent chat spam after conversations
* [ ] Regex checking of condition/event/objective instruction string syntax (to easily catch every error)
* [ ] Optionally requiring specific responses in chat during conversations (for riddles and stuff)
* [ ] Potion brewing objective (kinda hard to do or I'm stupid) (yeah, probably the second one...)
* [ ] Put item in chest objective (for crazy Skyrim-like delivery quests (eg. food for Greybeards))
* [ ] Logging errors to the file
* [ ] GUI or in-game, chat-based editor (it will take a while)
