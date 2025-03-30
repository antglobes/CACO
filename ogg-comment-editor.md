
# OGG Comment Editor (Created by antglobes)

- This exists as to document the proccess of how this tool got created as well
as archiving some of the older tools which are harder to find, often times the
 idea you have is possible you just have to be able to adapt to the realities
 of your limitations.

## Why this exists (a.k.a why not just use savt)

TLDR: Computer Autism

Actual Answer:

- Original Discussion in Anomaly Discord [here](https://discord.com/channels/456765861953536020/463899353480691738/1339618597768527872)
- I wanted a way to convert audio files to the ogg vorbis anomaly uses for audio 
programmatically so that i could add music via a script so that music could be
played while the game runs rather than having to create and modify the ogg 
files prior to running the game like in any addon that adds new music for 
the radio.
- The Conceptual Workflow based on this idea:
get a list of sound files with their path, convert them to ogg, write a default
ogg comment, fix it's hex so it's valid, load them into the engine just like
the already existing sounds are, have a script that manages playback.
- Kindly @ravenascendant pointed me towards vorbiscomment.exe and my research
would kick off from there, however from taking a glance i couldn't see an imple-
mentation that would fit into the ecosystem of anomaly's codebase and this would
have to be a totally seperate system that would ultimately lead me down the same
path as someone doing a radio addon, something that i wanted to avoid.
- Taking a few hours, later that same day i would realise that the main issue
was making the changes to the ogg's header aka the ogg comment, this is the part 
that informs the XRAY engine on how the sound should be treated aka it's parameters
(distance that the sound can be heared, it's type, for more info check [here](https://igigog.github.io/anomaly-modding-book/modding-tools/savandt.html))
- Something that wasn't entirely relevant for the audio file convertion and
comment editing itself but more so adding sounds dynamically via script:
i asked if a sound_object (the engine class that allows for sound playback) could
be added mid game via path rather than be loaded from game start like a config, texture,
script, mesh (model) would be. Once again the kind ravenascendant stated that as long
as it isnt played by the engine but by script this is possible; further solidifying
the possibility that i could create the aforementioned system.

- If you are familar with file conversion on any standard, you probaly have come across ffmpeg
and even so more likely to have used it at some point. Myself having used it many times on the
command line and it's python bindings, i simply thought it was a case of taking any audio file
and choosing ogg as the output. I was wrong, in order to convert to ogg without issues, first the
audio has to be converted to wav then to ogg. I also thought this would be enough but i was wrong
again, as anomaly or rather the x-ray engine has a special use case for using ogg as it's audio 
file format. Before check this out my second to last stop with ffmpeg was to check out the libavcodec
module of ffmpeg's source code but i didn't get that far being inexperienced with c languages.

- Having no luck with ffmpeg, i tried looking elsewhere. Being up there in terms of years a game
has a modding scence and seeing how many other elements for modding the sdk, some editors etc
have been continuious worked on as in new version have arrised over time, i figured their had to 
be a working predecessor to savt in which also had source code.

- I Started of [here](https://www.metacognix.com/files/stlkrsoc/index.html) (see 
bottom of the site, if unavailable check the wayback machine) from the features list it quickly
became apparent as to why the ffmpeg conversion process didn't work as intended, i needed to fix
the checksum after conversion but with the stock savt it works through a executable with an attached
gui. A shot in the dark but i started searching google with the author's name (NatVac) to see if
i could gain access to the source code of savt, to start implementing my idea.

- After a few hours or days rather, spent scrubbing the internet i searched "stalker ogg
comment editor" and came across a few sites.

  1. oggcomments.exe, found on stalker.pl (polish stalker forum 2004-2024~)
     - Published by YourEnemy on 1st April 2010 02:26
     - This works by taking the unpacked sounds folder, recursively wrting out the hex and the
     relative path from the sounds folder to the file and wrting this to a text file.
     - The idea is that if you have a weapon or item that has invalid ogg files, you take the hex
     and path for a similar ogg (similar use case, i.e copying gauss reload entry to your railgun entry)
     - I tried this myself and still managed to run into issues of having invalid ogg comments however 
     for archiving purposes you can find the page [here](https://forum.stalker.pl/viewtopic.php?f=78&t=8529&hilit=ogg+komentarze)
     on the [wayback machine](https://web.archive.org/web/20250217181756/https://forum.stalker.pl/viewtopic.php?f=78&t=8529&hilit=ogg+komentarze)
     and i will have the source code posted on my github [here](https://github.com//antglobes//ogg-comment-editor)


  2. oggcommentfix.exe, found on terverl.livejournal.com (russian social media)
     - Published by tervel on 2nd March 2014
     - This is the 1st version of the ogg comment editor by tervel, it's a command line tool
     capable of changing indiviual ogg files and adding "comments" into the header and correcting the checksum
     without any additional resources
     - This is essentially what i was looking for, all it took was a little time and research, there is even source
     code however, i did find a second version that was updated so i looked into this rather than explore the source
     code here.
     - Can be found [here](https://tervel.livejournal.com/7266.html) or at the wayback machine [here](https://web.archive.org/web/20240603054514/https://tervel.livejournal.com/7266.html)
     and the files found on the page at my github [here](https://github.com/antglobes/Stalker-Anomaly-OGG-Editing)

  3. OGGCEditor.exe, found on terverl.livejournal.com (russian social media)
     - Published by tervel on 10th February 2015
     - This is the 1st version of the ogg comment editor by tervel, this time it uses a GUI for interacting with
     the ogg comment editor, being able to automatically fix invalid oggs alongside setting the parameters for
     the comment itself. 
     - Once again Tervel kindly provided us with source code, although from the first few glances i was overwhelemed
     with the nature of the script, there's alot going on in there, however after going over it a few times
     i was able to figure out that the updated ogg mainpulation part of the script had been intergrated into the 
     windows gui, all it would take is to frankenstein the ogg mainpulation part into a new script.
     - can be found [here](https://tervel.livejournal.com/7266.html) or at the wayback machine [here] and
     the file found on the page [here](https://github.com/antglobes/Stalker-Anomaly-OGG-Editing)

- Having found a great example with the 3rd ogg comment editor, i would use this as a utility in overall
workflow where it would be able to maanage comment editing. Unsure of how i'd actually turn this idea into
working example, i still believed that doing this via script was possible or at least made sense. I 
orginally thought of this after seeing the buttplug addon (yes that's a real [addon](https://github.com/abbihors/buttplug-anomaly))
where the author abbihors took advantage of luajit (anomaly's scripting lanaguage) ffi feature where pure c
can be exported to lua (in their case using the pollnet socket library), i could possible do the same for
the scripts from OGGCEditor however since lua doesn't have any audio libraries capable of sound conversion,
(or at least i couldn't find any) plus ffmpeg in c being too convuluted, as well as anomaly having popen being
disabled, i decided against this. 

- Essentially believing this idea would come to a standstill like many mod ideas before it, i but this to rest
for a few days. But i remember that the author of the stalker helper [here](https://github.com/Thial/StalkerModdingHelper) Thial had managed to get anomaly
to run, so i would look into his implementation to see if i could do the same excecept in my case use whatever
they did do run ffmpeg. Looking into the source code for v1.1.0 i could see Thial had done this via processes
a straightforward approach which i could implement myself.

## My Implementation

The Conceptual Workflow:

- Step 1: File Conversion. Audio file -> Wav -> ogg
- Step 2: Ogg Comment Writing. Newly created ogg + Ini with comment values -> exported ogg comment function (oggnav) via dll -> update ogg with the comment
- Step 3: Move Files. Ini with output location -> Newly updated oggs with comments -> Move to gamedata/sounds dir

Functionality:

Taking inspiration of Thial's exe, i sought to split my implementation into 3 parts: ini (config file) that would
take, the gamedata directory (to be used for output and moving the files), the location of the ffmpeg binary,
input directory (where the audio files are to be sourced from); a ddl of the rewritten OGGCEditor so that i could
access the ogg comment editor from the c# script; the c# script itself that acts as the driver in this case
grabbing the files, converting, adding the comment and moving them to the output directory. This was suprisingly
easier than i had expected, perhaps it was due to my familiarity with java (i know they are different languages), 
but c# and java are quite similar in certain aspects.

I expanded this to be able to take in the comment parameters from the ini rather than be hardcoded so that this can
be set at the user's disrection.

The First version posted on github was specifically intended to be used to add playlists to the radio but as to
expand the useablility, i will make this alot more generalised, so that the user can configure the outputs to their
own needs.

If you are interested in making changes or simply just curious you can find the tool [here](https://github.com/antglobes/ogg-comment-editor)