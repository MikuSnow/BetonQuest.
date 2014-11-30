# Instalation and Configuration

## Compiling the plugin

You need to have JDK for version 1.7 or above, Git and Maven installed. Clone BetonQuest repository to some directory and issue command `mvn package` inside it. The .jar package should appear in _target_ directory.

## Installation

First of all you should install Citizens plugin. You can find it on it’s [dev.bukkit.org](http://dev.bukkit.org/bukkit-plugins/citizens/) page. It's not required, you can use NPCs made from block but it's less immersive. Download the BetonQuest plugin, place .jar file in your plugins folder, start and stop the server. BetonQuest generated configuration files. If you want to use MySQL for data storage then open config.yml and fill your database informations. If not, just leave these fields blank, the plugin will use SQLite instead. Now you can start the server. Now let's start with learning basics of BetonQuest's mechanics.

## Configuration

**Do not touch "version" option!**

There are several options in config.yml file. First is connection data for MySQL database. These are pretty straightforward. Metrics will define if your server will send anonymous data about the plugin and amount of players to mcstats.org. I highly recommend leaving it 'true', as I like to see that someone is using BetonQuest. UUID - if set to true the plugin will use UUIDs to store information about players, if false it will use names. Dont set to true if you run pre 1.7.5 server! If you want to manually convert names to UUIDs set this to true and add another option, "convert: true". Conversion will start on next plugin reload (eg. /q reload). Language is just translation of the plugin. Currently there are 4 available languages, English (en), German (de), French (fr) and Polish (pl). Default journal slot is a slot number in which the journal will appear. Default is -1 (last possible slot). Max NPC distance is the distance from NPC in which a conversation will end if player goes away. Global locations is list of location objectives’ IDs which are considered as global.
