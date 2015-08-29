# Commands and permissions

## Commands

* **/j** - gives the journal
* **/backpack** - opens the backpack
* **/q** - lists all available admin commands
* **/q reload** - reloads the plugin
* **/q objectives \<playerName\> [list/add/del] [instruction]** - shows player's currently active objectives
* **/q tags \<playerName\> [list/add/del] [tag]** - lists all player's tags
* **/q points \<playerName\> [list/add/del] [category] [amount]** - lists all player's points in all categories
* **/q journal \<playerName\> [list/add/del] [package.pointer] [date]** - lists 
* **/q event \<playerName\> \<package.eventID\>** - fires an event for the player
* **/q condition \<playerName\> \<package.conditionID\>** - shows if the player meet specified condition or not
* **/q item \<package.itemID\>** - creates an item based on what you're holding in hand
* **/q config \<set/add/read\> \<path\> [value]** - sets, adds or reads values from configuration
* **/q purge \<playerName\>** - deletes all player's data from the database
* **/q backup** - creates a backup of configuration files and database
* **/q create \<package\>**: creates new package with given name, filled with default quest
* **/q vector \<packname.variable\> \<newvariable\>**: calculates the vector from first location variable to you position and saves it as second variable
* **/questlang \<lang\>** - changes the language for the player (and globally if used from console). `default` language will use the language defined in _config.yml_.

## Aliases

* **/j**: bj, journal, bjournal, betonjournal, betonquestjournal
* **/backpack**: b, bb, bbackpack, betonbackpack, betonquestbackpack
* **/q**: bq, bquest, bquests, betonquest, betonquests, quest, quests
    * **objective**: o, objectives
    * **tag**: t, tags
    * **point**: p, points
    * **event**: e, events
    * **condition**: c, conditions
    * **journal**: j, journals
    * **item**: i, items
    * **create**: package
* **/questlang**: ql

## Permissions

* **betonquest.admin** - allows using admin commands (/q ...) and creating an NPC from blocks
* **betonquest.journal** - allows using /j command (default for players)
* **betonquest.backpack** - allows using /backpack command (default for players)
* **betonquest.conversation** - allows talking with NPCs (default for players)
* **betonquest.language** - allows changing the language (default for players)

## Main command details

Reloading loads all data from configuration, but not everything is updated. Player's data isn't touched to avoid lags made by database saving. The database is also the same, you will have to reload/restart the whole server for the database to change.

Tags subcommand allows you to easily list and modify tags. '`/q tags Beton`' would list tags for player Beton. '`/q tags Beton add test`' would add "test" tag for that player, and '`/q tags Beton del test`' would remove it.

Points subcommand is similar - listing points is done the same way. Adding points to a category looks like that: '`/q points Beton add reputation 20`' (adding 20 points to "reputation" category). You can also subtract points with negative amounts. Removing the whole point category can be achieved by '`/q points Beton del reputation`'.

Journal subcommand works in the same way as those two above. Adding and removing looks like `/q journal Beton add default.wood_started` (or `del`), and you can also specify the date of entry when adding it, by appending date written like this: `23.04.2014_16:52` at the end of the command. Note that there is `_` character instead of space! Name of the entry must be prefixed with a package name, because commands don't belong to any package.

Objective subcommand allows you to list all active objectives (shown as their labels) of the player. It can also directly add or cancel objectives using instruction strings. Remember to always prefix all events/conditions with package names if using command! If you want to add objective defined in _events.yml_ just use event subcommand.

Running events for online players can be done with event argument: '`/q event Beton default.give_emeralds`' would run "give_emeralds" for player Beton (if he's online) from "default" package. There is also condition argument for checking conditions, for example '`/q condition Beton default.has_food`'. Events and conditions need to be defined in their files, this command doesn't accept raw instructions. You can skip package name, the plugin will assume you're reffering to package specified in `default_package` option in _config.yml_ file.

If you need to create for example "Nettlebane" quest item, just hold it in your hand and type '`/q item default.nettlebane`'. It will copy the item you're holding into the _items.yml_ file and save it there with the name you specified (in this case "nettlebane"). You can skip the package name here as well.

Config subcommand is used to modify or display values in configuration files. `set` option replaces the value with what you typed, `add` simply adds your string to the existing value. (Note on spaces: by default the plugin won't insert a space between existing and added value. You can however achieve that by prefixing the string with `_` character. For example: existing string is `objective location`, and you want to add `100;200;300;world;10`. Your command will look like `/q config add default.events.loc_obj _100;200;300;world;10`). `read` option allows you to display config value without modifying it.

Path in this command is like an address of the value. Next branches are separated by dots. For example language setting in main configuration has path `config.language`, and a text in "bye" player option in default quest has path `default.conversations.innkeeper.player_options.bye.text`

You can purge specific player with '`/q purge Beton`' command. Currently there is no way of purging the entire database from command, but you can do that easily by changing the prefix used by the database.

If you want to backup your configuration and database make sure that your server is empty (this process requires all data to be saved to database -> all players offline) and run '`/q backup`' command. You will get a zip file containing all your data, ready to be unzipped for restoring the plugin.

Using '`/q create beton`' command you will create new package named '`beton`'. It will contain the default quest.

The `/q vector` command allows you to create vector variables from the specified in first argument location variable to your position. The result will be saved to the "vectors.{second argument}" variable.
