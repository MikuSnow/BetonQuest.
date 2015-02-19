# Frequently Asked Questions

If you have any questions please read it first. It's very likely that it has been already asked and answered. If not, feel free to make an Issue or a comment on any of plugin's pages across the Internet.

***

**Q**: _Do you have some quest samples or video tutorials?_

**A**: Unfortunatelly there's only documentation and the default quest at the moment. I will record some tutorials in the future but for now you just need to study these two sources.


***

**Q**: _When I first install this plugin it gives me strange errors saying that it could not read messages.yml because of special characters being not allowed..._

**A**: Your server doesn't support UTF-8 encoding. That means that you probably can't use characters like **ś**, **ł**, **¿** and others. To enable this you should add `-Dfile.encoding=UTF8` to your starting script. It's that script which you use to start your server (typically named `run.bat` on Windows and `start.sh` on Linux). There should be one line starting with `java -jar` or something like that. Add `-Dfile.encoding=UTF8` somewhere after `-jar`. If you don't have access to starting script, then ask your hosting to change that for you. It they refuse you - it's time to change the hosting. No, really, they are not professional if they won't change such a simple thing.

***

**Q**: _Where is a command for creating quests?_

**A**: There is no such command, nor there will be. As of today you need to edit the files directly, I'm sorry. The process of writing advanced quests cannot be as easy as in simple Quests plugins, so it would be even harder to do it with commands. I am planning however to code a web-based editor, which would be run similarly to [Dynmap](http://dev.bukkit.org/bukkit-plugins/dynmap/).

***

**Q**: _Would you add X feature?_

**A**: Check again if it's not already added. I have already got 6 such requests, 3 of them were about MySQL support (which was by the way implemented right after starting the development). If there is no such feature, and it doesn't involve PvP in any way then I can add it.

***

**Q**: _Why not PvP? :disappointed:_

**A**: I don't like it. And yes, because of that I'm terrible at it. Go and write an addon yourself.

***

**Q**: _Conversations are not working! I created NPC "Innkeeper" and he won't talk to me._

**A**: Conversations are not linked to an NPC through names, as you can have multiple Innkeepers. You need to connect them with their ID using "npcs.yml" file. Read [this](https://github.com/Co0sh/BetonQuest/wiki/Other-important-stuff#npcs).

***

