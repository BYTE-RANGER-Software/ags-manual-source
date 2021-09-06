## `Room` functions and properties

### `Room.Exists`

    static bool Room.Exists(int room)

Returns true if the specified room exists in the game.

Example:

    if(Room.Exists(10))
    {
      player.ChangeRoom(10);
    }

If room 10 is valid, go to that room.

*Compatibility:* Supported by **AGS 3.6.0** and later versions.

### `Room.GetDrawingSurfaceForBackground`

    static DrawingSurface* Room.GetDrawingSurfaceForBackground(optional int backgroundNumber)

Gets a drawing surface for a room background, which allows you to
directly draw onto the room's background image. You can provide a
background frame number if you want to modify a specific frame;
otherwise, the current background's surface will be returned.

After calling this method, use the various
[DrawingSurface functions](DrawingSurface) to modify the background,
then call Release on the surface when you are finished.

Any changes you make will only last until the player leaves the room, at
which point they will be lost. If you need to make long-lasting changes,
you can either use this method in the Player Enters Room event, or
consider using an alternate background frame for the changed image.

**NOTE:** Drawing onto the room background can be slow, especially when
using the Direct3D driver. Do not use this command in
repeatedly_execute; make sure you only use this command when absolutely
necessary.

Example:

    DrawingSurface *surface = Room.GetDrawingSurfaceForBackground();
    surface.DrawingColor = 14;
    surface.DrawLine(0, 0, 50, 50);
    surface.Release();

draws a yellow diagonal line across the top-left of the current room
background, then releases the image.

*See also:*
[DrawingSurface.DrawLine](DrawingSurface#drawingsurfacedrawline),
[DrawingSurface.Release](DrawingSurface#drawingsurfacerelease)

---

### `Room.GetProperty`

*(Formerly known as global function GetRoomProperty, which is now
obsolete)*

    Room.GetProperty(string property)

Returns the custom property setting of the PROPERTY for the current
room.

This command works with Number properties (it returns the number), and
with Boolean properties (returns 1 if the box was checked, 0 if not).

Use the equivalent Room.GetTextProperty function to get a text property.

Note that you cannot retrieve room properties of other rooms - only the
current room can be checked.

Example:

    if (Room.GetProperty("CanBeAttackedHere"))
      Display("An evil monster lunges at you!");

will print the message if the current room has its "CanBeAttackedHere"
box ticked.

*See also:* [Room.GetTextProperty](Room#roomgettextproperty)

---

### `Room.GetTextProperty`

*(Formerly known as global function GetRoomPropertyText, which is now
obsolete)*

    static String Room.GetTextProperty(string property)

Returns the custom property setting of the PROPERTY for the current
room.

This command works with Text properties only. The property's text will
be returned from this function.

Use the equivalent Room.GetProperty function to get a non-text property.

Note that you cannot retrieve room properties of other rooms - only the
current room can be checked.

Example:

    String description = Room.GetTextProperty("Description");
    Display("The room's description: %s", description);

will retrieve the room's "description" property then display it.

*See also:* [Room.GetProperty](Room#roomgetproperty)

---

### `Room.SetProperty`

    static bool Room.SetProperty(const string property, int value)

Sets the new *value* for the custom *property* for the specified room.
Returns TRUE if such property exists and FALSE on failure.

This command works with Number properties (it sets the numeric value),
and with Boolean properties (sets FALSE is value is equal to 0, or TRUE
otherwise).

Use the equivalent SetTextProperty function to set new text property
value.

Note that you cannot set room properties of other rooms - only the
current room.

Example:

    Room.SetProperty("Darkness", 10);

will change room's "Darkness" custom property to 10.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See also:* [Room.SetTextProperty](Room#roomsettextproperty)

---

### `Room.SetTextProperty`

    bool Room.SetTextProperty(const string property, const string value)

Sets the new *value* text for the custom *property* for the specified
room. Returns TRUE if such property exists and FALSE on failure.

This command works with Text properties only. The property's text will
be changed to new value.

Use the equivalent SetProperty function to set a non-text property.

Note that you cannot set room properties of other rooms - only the
current room.

Example:

    Room.SetTextProperty("Description", "The Throne Room");

will change room's "description" property.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See also:* [Room.SetProperty](Room#roomsetproperty)

---

### `Room.ProcessClick`

*(Formerly known as global function ProcessClick, which is now
obsolete)*

    static void Room.ProcessClick(int x, int y, CursorMode)

Simulates clicking the mouse on the location (X,Y) on the screen, in the specified cursor mode. This "click" has special behavior in that it **only affects Room elements and characters** under given coordinates.
Any interactions attached to the first object found on given coordinates and matching the given cursor mode will be executed. Any non-room objects (GUI) will be **ignored**. Even if the coordinates happen to lie on a button, the simulated click will "pass through" that button as if it was not present.

Please note that this function accepts *screen* coordinates and not *room* coordinates. If there's no room viewport on screen at this location the function will fail.

The available cursor modes are the ones you define on your Cursors tab (but with eMode prepended to them). Usually these are eModeWalkto, eModeLookat, etc.

Example:

    Room.ProcessClick(100, 50, eModeLookat);

will simulate a click in the Look mode on screen co-ordinates (100, 50).

*See also:* [GUI.ProcessClick](GUI#guiprocessclick),
[Mouse.Click](Mouse#mouseclick),
[IsInteractionAvailable](Globalfunctions_General#isinteractionavailable),
[Hotspot.RunInteraction](Hotspot#hotspotruninteraction)

---

### `Room.BottomEdge`

    readonly static int Room.BottomEdge

Returns the Y co-ordinate of the bottom edge of the room, as set in the
Room Settings pane of the editor.

Example:

    Display("The current room's bottom edge is at %d.", Room.BottomEdge);

*See also:* [Room.LeftEdge](Room#roomleftedge),
[Room.RightEdge](Room#roomrightedge),
[Room.TopEdge](Room#roomtopedge)

---

### `Room.ColorDepth`

    readonly static int Room.ColorDepth

Returns the color depth of the room's background scene. This is
important if you want to use DrawImage, since any sprites that you draw
must be the same color depth as the room itself.

Example:

    Display("The current room background is %d-bit color.", Room.ColorDepth);

*See also:*
[DrawingSurface.DrawImage](DrawingSurface#drawingsurfacedrawimage)

---

### `Room.Height`

*(Formerly known as game.room_height, which is now obsolete)*

    readonly static int Room.Height

Returns the height of the room.

Example:

    Display("The current room size is %d x %d.", Room.Width, Room.Height);

*See also:* [Room.Width](Room#roomwidth)

---

### `Room.LeftEdge`

    readonly static int Room.LeftEdge

Returns the X co-ordinate of the left edge of the room, as set in the
Room Settings pane of the editor.

Example:

    Display("The current room's left edge is at %d.", Room.LeftEdge);

*See also:* [Room.BottomEdge](Room#roombottomedge),
[Room.RightEdge](Room#roomrightedge),
[Room.TopEdge](Room#roomtopedge)

---

### `Room.Messages`

*(Formerly known as global function GetMessageText, which is now
obsolete)*

    readonly static String Room.Messages[int message]

Gets the text of the specified room message. This is useful if you want
to store, for example, a room description in Message 1 in each room --
this property allows you to retrieve the text for that message from the
current room.

If an invalid message number is supplied, *null* will be returned.
Otherwise, the message contents will be returned.

Example:

    String message1 = Room.Messages[1];
    Display("Message 1 says: %s", message1);

will print the contents of room message 1.

---

### `Room.MusicOnLoad`

    readonly static int Room.MusicOnLoad

**This property is now obsolete.** It is still accessible for backwards
compatibility with old games.

Returns the music number that is set to play when the player enters this
room, as set in the "Room Settings" pane in the editor. If no music is
set for this room, returns 0.

Example:

    Display("The current room plays music %d when the player enters.", Room.MusicOnLoad);

---

### `Room.ObjectCount`

*(Formerly part of GetGameParameter, which is now obsolete)*

    readonly static int Room.ObjectCount

Returns the number of objects in the room.

Example:

    Display("The current room contains %d objects.", Room.ObjectCount);

---

### `Room.RightEdge`

    readonly static int Room.RightEdge

Returns the X co-ordinate of the right edge of the room, as set in the
Room Settings pane of the editor.

Example:

    Display("The current room's right edge is at %d.", Room.RightEdge);

*See also:* [Room.BottomEdge](Room#roombottomedge),
[Room.LeftEdge](Room#roomleftedge),
[Room.TopEdge](Room#roomtopedge)

---

### `Room.TopEdge`

    readonly static int Room.TopEdge

Returns the Y co-ordinate of the top edge of the room, as set in the
Room Settings pane of the editor.

Example:

    Display("The current room's top edge is at %d.", Room.TopEdge);

*See also:* [Room.BottomEdge](Room#roombottomedge),
[Room.LeftEdge](Room#roomleftedge),
[Room.RightEdge](Room#roomrightedge)

---

### `Room.Width`

*(Formerly known as game.room_width, which is now obsolete)*

    readonly static int Room.Width

Returns the width of the room.

Example:

    Display("The current room size is %d x %d.", Room.Width, Room.Height);

*See also:* [Room.Height](Room#roomheight)

