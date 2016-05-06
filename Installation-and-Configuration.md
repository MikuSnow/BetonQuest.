# Installation and Configuration

## Installation

First of all you should install Citizens plugin. You can find it on it’s [dev.bukkit.org](http://dev.bukkit.org/bukkit-plugins/citizens/) page. It's not required, you can use NPCs made from clay blocks, but that would be less immersive. Download the BetonQuest plugin, place `.jar` file in your _plugins_ folder and start the server. BetonQuest generated configuration files. If you want to use MySQL for data storage then open _config.yml_ and fill your database informations. If not, just leave these fields blank, the plugin will use SQLite instead. If you don't want to use autoupdater disable it in configuration before restarting the server or reloading the plugin. When you're finished you can reload the plugin (**/q reload**). Now tweak the configuration to your liking and move on to _Quick start tutorial_ chapter. You don't have to read about commands and permissions just yet, you should undestand how the plugin works first.

## Configuration

**Do not touch "version" option! _It may corupt your files!_**

There are several options in config.yml file. I will describe only those that you might want to set before using the plugin. The rest is described in appropriate sections of this documentation (i.e. `package` option is explained in _Other important stuff_ chapter, in _Packages_ topic). 

* First is connection data for MySQL database. Fill it to use MySQL, leave it blank to use SQLite.
* `update` section controls the updater. `enable` option is set to true by default and it controls if the plugin should do anything update-related. `download_bugfixes` controls if BetonQuest should automatically update bugfix versions (like _1.7.3 -> 1.7.4_ or _1.8.1 -> 1.8.3_). These versions **do not** change how the plugin works, they only fix bugs, so it's good to set it to `true`. `notify_new_release` option is responsible for displaying a notification at startup about new releases (like _1.7.6 -> 1.8_). These can change how the plugin works by introducing new features and changing existing ones, so they won't be downloaded automatically. You can use `/q update` when you're ready. If you're using a development version, there will be a third setting here, `notify_dev_build`. This is the same as `notify_new_release` but it checks the development builds instead. There are no specific version checking here, so if the found dev number is higher, it will appear. You download development builds on your own responsibility.
* Language is just translation of the plugin. Currently there are 7 available languages, English (en), German (de), French (fr), Spanish (es), Chinese (cn), Dutch (nl) and Polish (pl).
* Sounds define what sounds will be played on these occasions: `start` and `end` refer to starting/ending conversations. `journal` is just updating journal. `update` is played when there's a changelog file, to draw your attention. `full` can be played when the player uses /j command but his inventory is full. List of all possible sounds can be found [here](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Sound.html).
* `combat_delay` is a delay (in seconds) the player must wait before he can start the conversation after combat.
* `notify_pullback` will display a message every time the player is pulled back by the `stop` option in conversations.
* `default_package` is a name of the package that should be used when you don't specify package in /q command. It's for your convenience.
* `cmd_blacklist` is a list of commands that can't be used while in conversation. Remember that you can type here only single words!
* `hook` controls compatibility with other plugins. Here you can turn off each hook.
* `remove_items_after_respawn` option should be turned on if you don't use "keepInventory" gamerule. It prevents other plugins from duplicating quest items after death. When the player dies, his quest items are removed from drops and stored in the backpack, but some plugins may try to restore all items to the player (for example WorldGuard custom flag keep-inventory). That's why it's so important to remove the quest items that are in player's inventory after he respawns (they are also in backpack). The "keepInventory" gamerule however works differently - the items are never dropped, so they cannot be added to backpack. Removing them from the inventory would destroy them forever. Sadly, Bukkit does not allow for gamerule checking, so it's up to you to decide. Once again: if you have "keepInventory" gamerule set to true, this setting has to be false, and vice versa.
* `date_format` is the Java date format used in journal dates. It needs to have a space between the day and hour.
* `debug` is responsible for logging plugin's activity to _debug.log_ file in _logs_ directory. You shouldn't turn this on as it can slow your server down. However if you experience any errors turn this on, let the plugin gather the data and send logs to the developer. Note that first run of the plugin will be logged anyway, just as a precaution.

There is also `advanced-messages.yml` file. It contains translations with special characters. Not all servers are capable of displaying them, some will even crash the plugin, but your server can use them, just replace the content of original `messages.yml` with this file. Note that Chinese translation is only available in `advanced-messages.yml` file.

## Updating

The  updating process is safe and easy. After updating to a new version (manually or automatically) configuration files and database will be automatically backed up to a zip file so you never lose all your work due to an error. Then configuration will be converted to a new version. At the end the localization will be updated with new languages and the _changelog.txt_ file will be created for you.

When you enter the server BetonQuest will alert you about changes and ask you to read changelog.txt file located in plugin's main directory. This way you will be always up to date with every changes made by new versions.

All next versions of BetonQuest should have full compatibility with your current version of the plugin and server. This means that after updating the plugin should work _exactly_ the same way as it did before (except for bugs). The changes will be visible only in configuration format or new features (for example in 1.6 inverting conditions will be done with prefixing their name with `!` character instead of adding `--inverted` tag; updater will automatically convert all `--inverted` tags to `!`s in your configuration files and the plugin will work as expected; your only concern is not to use `--inverted` tag in conditions anymore, but you will be informed about it by changelog.txt file).

If there were any unexpected errors during an update process just download previous version, restore your configs from backup and disable autoupdating feature. Don't forget to post your error so I can fix it!

## Backups

Every time the plugin updates the configuration there is a backup created. This is especially important if you use development versions, as they may be unstable. You can also create a backup manually by running **/q backup** command. It needs to be run from console on empty server, because it heavily uses the database.

You can find your backups in _backup_ directory in plugin's folder. They are .zip files containing all your configuration and _database-backup.yml_ file, which - as the name says - is your database backup. If you want to replace your configuration with an older backup just delete all the files (except backups and logs) and replace them with the files from .zip file.

If you want your database loaded you should also place _database-backup.yml_ file in plugin's directory. When the plugin sees this file while enabling, it will backup the current database and load all data from that file to the database. You can find a backup of old database in _backups_ folder, so if you ever need to load it back, just rename it to _database-backup.yml_ and place it back in main plugin's directory. Note that _database-backup.yml_ file will be deleted after loading, so it doesn't replace your database on next plugin start.

## Migrating database from SQLite to MySQL and back

Follow these few simple steps to migrate your database easily:

1. Create a backup with **/q backup** command.
2. Extract database backup from it.
3. Turn your server off.
4. Place the _database-backup.yml_ file inside plugin's directory.
5. Edit in configuration which database type you want to use (correct credentials for MySQL, incorrect or empty for SQLite).
6. Start the server.
7. Check for errors.
8. If there are no errors, enjoy your migrated database.
9. If there are any errors, post them to the developer or try to fix them if you know how.