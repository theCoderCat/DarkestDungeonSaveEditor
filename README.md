# Darkest Dungeon Save Reader
DSON (Darkest JSON) to JSON converter.

There are still a few unknown variables in the file, in the code they're named with greek letters.


## Usage

    java -jar DDSaveReader.jar [--debug, -d] [--names, -n <namefile>] [--output, -o <outfile>] filename

`-d` dumps all metadata without known purpose as comments into the JSON file at the appropriate place.
This might come in handy when trying to find a pattern in them. With `-d`, the file is not valid JSON, but should be after removing all comments. Files translated without the `-d` flag should be valid JSON.

`-n` provides a Name File, a newline separated list of strings that are recognized as hashed values.
Darkest Dungeon hashes some strings using their own hash algorithm, which can make reading some files rather complicated for you. Whenever an integer is recognized as the hash of a given string, it's replaced with that String instead.
When combined with the `-d` flag, the hashed integers are added as comments.

A list can be compiled by running

    java -cp DDSaveReader.jar de.robojumper.ddsavereader.util.ReadNames [dir1] [dir2] [dir3] [...]

`dir1`, ... are directories that contain Darkest Dungeon game data. These are usually the game root directory, but can also be mods.  
There is no output file parameter, just pipe it to a file (append ` > names.txt`).

## Save File Model

The Application includes a save file watcher that automatically watches for changes to the save file and updates its internal save file model. This can be used to (for example) add a Twitch bot that can respond to queries by viewers. An example Twitch bot is provided, it can be run by setting the appropriate environment variables and starting the bot:

	SET DDSAVEDIR=
	SET DDCLIENTID=
	SET DDCLIENTSECRET=
	SET DDTOKEN=
	SET DDCHANNEL=
	
	java -cp de.robojumper.ddsavereader.twitchbot.DDSampleTwitchBot 
	
However, you are free to use your own bot implementation, the save file watcher and model are separated from the bot itself.

## Download

[Releases Page](https://github.com/robojumper/DarkestDungeonSaveReader/releases/)

## Plans

* Figure out unknown variables
* Expand to edit / save functionality

## Attribution

This application uses the [Google GSON Library](https://github.com/google/gson) 2.8.5, licensed under the [Apache License 2.0](https://github.com/robojumper/DarkestDungeonSaveReader/blob/master/Licenses/Apachev2.0.txt).

This application uses the [twitch4j Library](https://github.com/twitch4j/twitch4j) 0.10.2, licensed under the [MIT LICENSE](https://github.com/robojumper/DarkestDungeonSaveReader/blob/master/Licenses/MIT.txt).
