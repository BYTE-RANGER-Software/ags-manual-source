## The run-time engine

The engine (also called the "interpreter") is what runs your game and is
what the player will use.

You can use any port of the AGS runtime on any available system to run an AGS game data. 

Desktop systems, like Windows, Linux and MacOS offer a command line interface.

On Android, there's a special version of the runtime called AGS Player, and it's available with AGS releases. The web version of AGS, also can be used as a runtime, but currently it offers no graphical setup options. 

### Command line

*Note:* On Windows, you **must** use `--console-attach` when you are on the `cmd.exe` or other windows prompt and want to 
read the output of the ags runtime directly in the terminal, as printed in stdout.

General usage: `ags [OPTIONS] [GAMEFILE PATH or GAME DIRECTORY]`
(Where "ags" is the executable name)

Following OPTIONS are supported when running from the command line:

* `-? / --help` - prints the most useful command line arguments and quits.
* `-v / --version` - prints the engine version and quits.
* `--clear-cache-on-room-change` - clears sprite cache on every room change
* `--conf <FILEPATH>` - specify an explicit config file to read on startup.
* `--console-attach` - write the output to the parent process's console (Windows only).
* `--fps` - display fps counter.
* `--fullscreen` - run in fullscreen mode.
* `--gfxdriver <name>` - use specified graphics driver:
  * d3d9 - Direct3D9 (MS Windows only);
  * ogl - OpenGL;
  * software - software renderer.
* `--gfxfilter \<name\> [ \<game_scaling\> ]` - use specified graphics filter and scaling factor.
  * filter names:
    * none - run in native game size;
    * stdscale - nearest-neighbour scaling;
    * linear - anti-aliased scaling; not usable with software renderer.
  * game scaling:
    * proportional, round, stretch,
    * or an explicit integer multiplier (applied only to the windowed mode).
  * Examples:
    * `--gfxfilter stdscale 2` - applies round x2 scaling (window twice the size of the game);
    * `--gfxfilter stdscale round` - applies max round scaling;
    * `--gfxfilter stdscale proportional` - applies max stretch while keeping aspect ratio.
* `--loadsavedgame <filepath>` - load savegame on startup.
* `--localuserconf` - read and write the user config in the game's directory rather than using the standard system path. The game directory must be writable.
* `--log-OUTPUT=GROUP[:LEVEL][,GROUP[:LEVEL]][,...]`;
* `--log-OUTPUT=+GROUPLIST[:LEVEL]` - setup logging to the chosen OUTPUT with the given log groups and verbosity levels;
  Groups may be defined either by name or by a LIST of one-letter IDs, preceded by '+', e.g. +ABCD:LEVEL. Verbosity may be defined either by name or a numeric ID.
  * `OUTPUTs` are:
    * `stdout`, `file`, `console` (where \"console\" is internal engine's console);
  * `GROUPs` are:
    * `all`, `main` (m), `game` (g), `manobj` (o), `sdl` (l), `script` (s), `sprcache` (c);
  * `LEVELs` are:
    * `all`, `alert` (1), `fatal` (2), `error` (3), `warn` (4), `info` (5), `debug` (6);
  * Examples:
    * `--log-file=all:warn`
    * `--log-file=main:warn,game:all`
    * `--log-stdout=+mg:debug`
* `--log-file-path=PATH` - define a custom path for the log file.
* `--no-message-box` - disable alerts as modal message boxes (Windows only).
* `--noiface` - don't draw game GUI (for test purposes).
* `--noscript` - don't run room scripts (for test purposes); *WARNING:* unreliable.
* `--nospr` - don't draw room objects and characters (for test purposes).
* `--noupdate` - don't run game update (for test purposes).
* `--novideo` - don't play game videos (for test purposes).
* `--rotation <MODE>` - screen rotation preferences. MODEs are:  unlocked (0), portrait (1), landscape (2).
* `--sdl-log=LEVEL` - setup SDL's own logging level (see explanation for the related config option).
* `--setup` - run integrated setup dialog. Currently only supported by Windows version.
* `--shared-data-dir <DIR>` - set the shared game data directory. Corresponds to the "shared_data_dir" config option.
* `--startr <room_number>` - start the game by loading a certain room (for test purposes).
* `--tell` - print various information concerning engine and the game, and quit. Output is done in INI format.
  * `--tell-config` - print contents of a merged game config.
  * `--tell-configpath` - print paths to available config files.
  * `--tell-data` - print information on game data and its location.
  * `--tell-gameproperties` - print information on game general settings.
  * `--tell-engine` - print the engine name and version.
  * `--tell-filepath` - print all filepaths the engine uses for the game.
  * `--tell-graphicdriver` - print a list of supported graphic drivers.
* `--test` - run the game in the test mode, unlocking test key combinations and console.
* `--translation` - select the given translation on start.
* `--user-data-dir <DIR>` - set the save game directory. Corresponds to "user_data_dir" config option.
* `--windowed` - run in windowed mode.


Command line arguments override options from either configuration file where applicable.


*See also:* [Default setup (Editor Pane)](DefaultSetup), [Run-time engine setup](Setup)