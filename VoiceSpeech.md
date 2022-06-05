## Voice speech

With AGS you can link a line of dialog to a speech file, to enable
"talkie"- style games. Suppose you have a dialog script with the
following content:

    ego: "Hi! How are you?"
    michael: "I'm fine."

Normally this would display the words in the speech text above the
characters heads. However, you can add the special character '&' to
symbolize that a voice file should be played along with the displayed text.

The file name has the format XXXXY.EXT, where XXXX comes from the **first
four letters** of the character's script name (except the leading 'c'),
the Y is the speech file number (with no leading or trailing zeroes or
padding of any kind), and EXT is the file extension.

For example, if you have dialog script:

    ego: &10 "Hi! How are you?"
    michael: &7 "I'm fine."

or common script using Say script function:

    cEgo.Say("&10 Hi! How are you?");
    cMichael.Say("&7 I'm fine.");

Both of those examples plays EGO10.WAV with the first line, and
MICH7.WAV with the second. When a line of text has a voice linked to it,
the text on the screen will not be removed until the voice file has
finished playing. If the player interrupts it by clicking the mouse or
pressing a key, the text and voice will be stopped. Voice files must be
placed in the "Speech" sub-directory of the game folder.

**NOTE:** Speech file numbers are restricted to the positive range of 1 to 2147483647 (2 billion). This is a technical limitation based on how these are handled inside the engine, but we do not think that running out of numbers to use will ever become a problem to the user.

### Voice packs

Any sound format supported by AGS can be used for speech as well.

AGS uses separate voice packs to store the speech files. The default voice pack is compiled by placing audio files in the "Speech" sub-directory of the game folder, and is named "speech.vox".

Since version 3.6.0, AGS also supports multiple alternate voice packs. These are compiled from *subdirectories* nested inside the "Speech" folder, and are named "sp_DIRNAME.vox", where DIRNAME is the name of that subdirectory.
The speech files in these alternate directories must have the same names as files in the "Speech" directory itself. These extra packs are used to provide voice-over for different languages.

For example, if you have this folder structure in your game project:

* Speech
* * Francais
* * MyLang

then the editor will create following voxes:
* speech.vox (with files only from the root "Speech" folder);
* sp_francais.vox (with files from "Speech/Francais");
* sp_mylang.vox (with files from "Speech/MyLang");

**NOTE:** only top-level files are included into the voice pack, any further subfolders are ignored.

Since AGS 3.6.0, the engine supports switching to a different speech vox anytime. To do so, there's a new script function [Game.ChangeSpeechVox](Game#gamechangespeechvox).

Note that the voice packs are considered optional, and your game will function correctly even without them, in case there is no voice pack, the game will display speech text but play no voice. This makes it possible for the game author to offer voice packs as an optional download for the players.
If a particular speech file is missing from a voice pack, that will not not cause game errors and display just the text on screen.

*SeeAlso:* [`Game.ChangeSpeechVox`](Game#gamechangespeechvox),
[`Speech.VoiceMode`](Speech#speechvoicemode)