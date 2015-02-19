# Commands and permissions

## Commands

* **/j** - gives the player a copy of his journal
* **/q** - lists all available admin commands
* **/q reload** - reloads the plugin
* **/q purge \<nick\>** - deletes all player's data from the database
* **/q objectives** - shows your currently active objectives
* **/q tags** - lists all your tags
* **/q points** - lists all your points in all categories
* **/q event \<eventID\> [playerName]** - fires an event (playerName is optional)
* **/q item \<itemID\>** - creates an item based on what you're holding in hand
* **/q condition \<conditionID\>** - shows you if you meet specified condition or not
* **/q backup** - creates a backup of configuration files and database; can be used only on empty server, from the console

## Aliases

* **/j**: bj, journal, bjournal, betonjournal
* **/q**: bq, bquest, bquests, betonquest, betonquests, quest, quests
    * **objectives**: o, obj, objective
    * **tags**: t, tag
    * **points**: p, point
    * **event**: e, events
    * **condition**: c, conditions
    * **item**: i, items

## Permissions

* **betonquest.admin** - allows using admin commands (/q ...) and creating an NPC from blocks
* **betonquest.journal** - allows using /j command (default for players)
* **betonquest.conversation** - allows talking with NPCs (default for players)
