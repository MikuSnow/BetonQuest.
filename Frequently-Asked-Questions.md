# Frequently Asked Questions

If you have any questions please read it first. It's very likely that it has been already asked and answered. If not, feel free to make an Issue or a comment on any of plugin's pages across the Internet.

***

**Q**: _Would you make conversation options clickable?_

**A**: Open _config.yml_ file and set `default_conversation_IO` option to "tellraw". You can also set it to "chest" if you want conversations to be displayed in an inventory GUI.

***

**Q**: _Will you add particles over NPCs' heads like in `Quests` plugin?_

**A**: [Yes, I will, eventually.](https://github.com/Co0sh/BetonQuest/issues/2)

***

**Q**: _The players don't know they have to end a conversation, could you add "auto-ending" when walk away?_

**A**: Set `stop` option to "false" in conversation file.

***

**Q**: _I have an error which says "Cannot load plugins/BetonQuest/\<packName\>/conversations/\<conversation\>.yml", what is wrong?_

**A**: You have incorrect YAML syntax in your conversation file. Check it with [YAML Lint](http://yamllint.com) to see what's wrong. Usually it's because you start a line with `!` or `&`, forget colons or make some weird things with apostrophes.

***

**Q**: _Where is a command for creating quests?_

**A**: There is no such command, nor there will be. As of today you need to edit the files directly, I'm sorry. The process of writing advanced quests cannot be as easy as in simple Quests plugins, so it would be even harder to do it with commands. I am planning however to code a desktop editor.

***

**Q**: _Conversations are not working! I created NPC "Innkeeper" and he won't talk to me._

**A**: Conversations are not linked to an NPC through names, as you can have multiple Innkeepers. You need to connect them with their ID. Read [this](https://github.com/Co0sh/BetonQuest/wiki/Reference#npcs).

***

**Q**: _I saved a book with a command, but `item` condition is not working on it!_

**A**: This is caused by a bug (or an undocumented feature, call it like you want) in 1.8 servers. The detailed instruction on how to work it around is in "Reference" chapter, in the part about items.

***
