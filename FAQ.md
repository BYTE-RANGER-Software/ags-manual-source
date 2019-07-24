## Frequently Asked Questions

This section of the manual is very rarely updated. Please consult the
AGS Forums on the website -- in particular, the Beginners Technical
Forum has an excellent Beginners FAQ (the "BFAQ") which is much more
extensive and is updated regularly with all sorts of Q&A's.

**Q. What's the deal with the license?**

A. The software is provided under [Artistic License 2.0](https://opensource.org/licenses/artistic-license-2.0.php).

**Q. On my screen, I can't move the main character. Wherever I click to
move him, he just stands there.**

A. If the main character isn't on a walkable area, he will not be able
to move. Load the room in the editor, and check that the location where
the character starts is on a walkable area.

**Q. I am looking/interacting with an object but nothing happens, but I have it on the script file.**

A. In the AGS Room Editor, under the object properties, in events, the field should be filled with the function to execute, wiring the room element to the script. If it's empty, clicking on the three dots button (...) the respective script will be open with the a new function for you to fill the details. If it has a value, clicking on the same button will direct you to it on the respective script file. This is true for all events, so for example a 'room_Load' script function won't trigger if it's not wired on the room events. It's usually easier to click on the three dots button of the event you want to develop in the Room Editor, which will generate the function on the script file for you to fill up.

**Q. I click on a GUI button, but nothing happens. It doesn't seem to register clicks!**

A. There are some different immediate suspects here. 
- Is the button set to Run Script? Go to the GUI Editor, select the button, and make sure that in its properties window, "Left Click" is set to "Run Script".
- Is the GUI clickable? While in the GUI Editor, make sure that the "Clickable" checkbox at the top is checked for the GUI that the button is on.
- Alternatively, if you are creating many GUIs, check if you have created a transparent, clickable GUI that is on top of the GUI you are clicking.
- Is your script in the right function? You need to put your script inside the `interfaceName_click` function in the global script, and the event must be wired on the GUI Editor.

**Q. When I enter a certain room, I just get a black screen.**

A. Make sure that you haven't used a Display Message command in the
"Enters room before fade-in" event for that room. Remember that this
event happens BEFORE the screen fades in.

To make sure, when you get the black screen, try pressing enter, or
clicking the left mouse button. If nothing happens then something more
serious may have happened. If this is the case, press Alt+X, which
should exit the program and allow you to trace which line of script it
has stopped on.

**Q. The character isn't drawn behind my walk-behind areas!**

A. You need to define the base line for the area, or he will always be
drawn in front. See the tutorial for more information.

**Q. Can I use script commands on my dialogues?**

A. Yes, you can. The dialog lines that start with at least one space character are interpreted as plain script, and the ones that don't are treated as special dialog commands. All special dialog commands are actually converted into real AGS script before compiling into your game.

**Q. My game EXE file seems to have disappeared.**

A. Because this file is your entire game, including the room files, when
you save a room in the Room Editor it will delete the exe file (because
the room contained in the exe is out of date). To get it back, simply
build the game again by using the "Build EXE" command on the Build menu.

**Q. What resolution should I make my game?**

A. This is asked a lot on the forums and you can browse through it. AGS games are not different from any other games. Think on what resolution is best for your chosen game design and graphic style.

**Q. How should I name my views, objects, ...**

A. When you are looking into your objects in the Room Editor, they are obviously an object. When you are referencing them on script, you can get lost. It's a good and common practice when using AGS to precede the name of an element with a lower case letter of it's type, make it easier to find them in the Editor with auto complete (ctrl+space) and the consistency will make easier to remember. So for a view, something like `vRogerWalking` is a good name, and the `v` at start tells you it's a view; A character with real name Joe, is a good idea to have the script name be cJoe, now the `c` reminds of character; a GUI for a lever puzzle could be called `gLeverPuzzle`; An object that is a flower as `oFlower`; A hotspot of the exit door as hExitDoor.