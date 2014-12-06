# Instalation and Configuration

## Installation

First of all you should install Citizens plugin. You can find it on it’s [dev.bukkit.org](http://dev.bukkit.org/bukkit-plugins/citizens/) page. It's not required, you can use NPCs made from block but it's less immersive. Download the BetonQuest plugin, place .jar file in your plugins folder, start and stop the server. BetonQuest generated configuration files. If you want to use MySQL for data storage then open config.yml and fill your database informations. If not, just leave these fields blank, the plugin will use SQLite instead. Now you can start the server. Now let's start with learning basics of BetonQuest's mechanics.

## Configuration

**Do not touch "version" option! _It may corupt your files!_**

There are several options in config.yml file. First is connection data for MySQL database. These are pretty straightforward. Metrics will define if your server will send anonymous data about the plugin and amount of players to mcstats.org. I highly recommend leaving it 'true', as I like to see that someone is using BetonQuest. AutoUpdate is set to false by default, if you want to allow the plugin to update itself as soon as next version will be uploaded to dev.bukkit.org set it to true. UUID - if set to true the plugin will use UUIDs to store information about players, if false it will use names. Dont set to true if you run pre 1.7.5 server! If you want to manually convert names to UUIDs set this to true and add another option, "convert: true". Conversion will start on next plugin reload (eg. /q reload). Language is just translation of the plugin. Currently there are 4 available languages, English (en), German (de), French (fr) and Polish (pl). Default journal slot is a slot number in which the journal will appear. Default is -1 (last possible slot). Max NPC distance is the distance from NPC in which a conversation will end if player goes away. Global locations is list of location objectives’ IDs which are considered as global.

## AutoUpdater

**To enable this feature set `autoupdate` to true in config.yml**

The auto updating process is safe and easy. When the next version of the plugin will be uploaded to dev.bukkit.org BetonQuest will download it and replace itself with newer version. On next reload/restart of your server it will be automaticly loaded.

Configuration files will be automatically backed up to a zip file so you never lose all your work due to an error. Then configuration will be converted to a newer version. At the end the localization will be updated with new languages and the cangelog.txt file will be created.

When you enter the server BetonQuest will alert you about changes and ask you to read changelog.txt file located in plugin's main directory. This way you will be always up to date with every changes made by new versions. All next versions of BetonQuest will have full compability with your current server version.

If there were any unexpected errors during an update process just download previous version, restore your configs from backup and disable autoupdating feature. Don't forget to post your error so I can fix it!