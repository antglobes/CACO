# CACO (Convert Audio Comment OGG)

Disclaimer:

- [Ffmpeg](https://www.ffmpeg.org/download.html) Must be installed to use this tool
- Only wav or mp3 files are accepted for conversion

## How to use

Setup the `config.ini` file with the relevant paths, place it in the same directory as the `caco.exe` and the `add_ogg_comment.dll` and either double click it to run or doing `.\caco.exe` in a command prompt.

See [here](ogg-comment-editor.md) for explanation on how caco functions.

## Config.ini Explanined

|Field|Purpose|Optional|Example|
|-----|-------|--------|-------|
|GamedataDir|Root Directory of where all addon related files will be stored|No|GamedataDir=C:\Stalker Dev\game files\gamedata|
|FfmpegBinDir|The Directory holding the ffmpeg executable file|No|FfmpegBinDir=C:\Users\tyres\ffmpeg\ffmpeg-2023-02-13\bin|
|InputDir|The Directory holding the audio files to convert|No|InputDir=C:\Users\tyres\OneDrive\Desktop\Input|
|OutputDir|The Directory in which the ogg files will be written to|Yes (GamedataDir + "\\Sounds" will be used if left blank)|OutputDir=C:\Stalker Dev\game files\gamedata\sounds|
|GameSndType|Part of the ogg comment, defines the type of sound that is played|No|GameSndType=world_ambient|
|BaseSndVol|Part of the ogg comment, defines how loud the sound will be|No|BaseSndVol=1.0|
|MinDist|Part of the ogg comment, Minimum Distance the sound can be heard|No|MinDist=1.0|
|MaxDist|Part of the ogg comment, Maximum Distance the sound can be heard|No|MaxDist=2.0|
|MaxAIDist|Part of the ogg comment, Maximum Distance that Npcs can pick up this sounds|No|MaxAIDist=1.0|
|RemoveWav|Delete the wav file after converting to ogg|Yes (will be false by default)|RemoveWav=true|

All values are floats but intergers work as well.
BaseSndVol must be between 0.0 - 2.0.
GameSndType can be any of the following:

- world_ambient
- object_exploding
- object_colliding
- object_breaking
- anomaly_idle
- npc_eating
- npc_attacking
- npc_talking
- npc_step
- npc_injuring
- npc_dying
- item_using
- item_taking
- item_hiding
- item_dropping
- item_picking_up
- weapon_recharging
- weapon_bullet_hit
- weapon_empty_clicking
- weapon_shooting
- undefined
