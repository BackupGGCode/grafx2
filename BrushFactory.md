# Introduction #

Grafx2 offers a lot of features, but sometimes you need something really
particular, and it's not there. That's why we added the brush factory, it allows you to generate or modify a brush using a lua script.
It has been expanded to allow changing the image and palette.
So you can extend Grafx2 capabilities with almost no limit!

We are looking forward to your scripts, please send us them so we can share them
in the next version of GrafX2!

# How does it work #

Using the brush factory is quite simple : just right click the 'brush effects' button to open it.
It's a small window allowing you to select the script you want to run.
Once you press the run button, the script is executed and generates something.
If it's a brush, you can paste it like any other brush. If it's a picture, you should see it.
If you create your own scripts and place them in _<program directory>/scripts_ they will appear in the list. Scripts are reloaded from disk when you run them, so you can edit them in a text editor and test them without leaving Grafx2.

# Available scripts #

Before you start working on your own script, you may want to have a look at the existing ones. Maybe one of them already does what you need. If you make your own script, you may want to send it to the developpers so other users can enjoy it too. It's possible to go quite far with scripts and do complicated things, from palette manipulation to animating a sprite sheet.

See the LuaScript list.

# API Reference #

Here is a list of things you get in lua. If you think we should add more, let us know !

## Conventions ##
On this page we use the following conventions :
  * x : horizontal position
  * y : vertical position
  * c : color index
  * w : width
  * h : height
  * r : red
  * g : green
  * b : blue

Note this is just for the examples below. You are free to name your variables the way you want.

## Functions ##
### Drawing ###
This is as simple as it gets. You can just render some things to the brush or to the current layer.

  * `putbrushpixel(x, y, c)` set the color of pixel at coords (x, y) in the brush to c.

  * `putpicturepixel(x, y, c)` set the color of pixel at coords (x, y) in the picture to c.

  * `putsparepicturepixel(x, y, c)` set the color of pixel at coords (x, y) in the spare picture to c.


  * `drawline(x1,y1,x2,y2,c)` draws a line in the picture.

  * `drawfilledrect(x1,y1,x2,y2,c)` draws a filled rectangle in the picture.

  * `drawcircle(x1,y1,r,c)` draws a circle in the picture. _r_ is radius in pixels.

  * `drawdisk(x1,y1,r,c)` draws a filled circle in the picture. _r_ is radius in pixels.

  * `clearpicture(c)` clears picture with color c.

Drawing out of bounds has no effect.

### Reading pixels ###
These allows you to read existing data, for example to filter it, do batch color replacing, or any other distorsion you could come up with.

  * `getbrushpixel(x, y)` returns the color of pixel at coords (x, y) in the brush.

  * `getbrushbackuppixel(x, y)` returns the color of pixel at coords (x, y) in the backup brush, before any of your changes.

  * `getpicturepixel(x, y)` returns the color of pixel at coords (x, y) in the picture. If there are several layers visible,this will pick "the color that you see".

  * `getlayerpixel(x, y)` returns the color of pixel at coords (x, y) in the current layer of the picture.

  * `getbackuppixel(x, y)` returns the color of pixel at coords (x, y) in the backup screen, that is, the picture before your script started to run.

  * `getsparelayerpixel(x, y)` returns the color of pixel at coords (x, y) in the current layer of the spare picture.

  * `getsparepicturepixel(x, y)` returns the color of pixel at coords (x, y) in the spare picture. If there are several layers visible, this will pick "the color that you see".


Reading out of the brush will return the BackGround color, ie. the one that marks transparent pixels in the brush.

Reading out of the picture will return the Transparent color.

### Changing sizes ###
Note the resize occurs immediately. If you need the original dimensions, to read from the backup, you should query them before the resize and keep them in Lua variables.

  * `getbrushsize()` returns the brush size (w, h).

  * `setbrushsize(w, h)` sets the brush size. The new brush is initially filled with transparent pixels.

  * `getpicturesize()` returns the picture size (w, h).

  * `setpicturesize(w, h)` sets the picture size. All layers are clipped accordingly. If you have made changes on the picture, you should call finalizepicture() first.

  * `getsparepicturesize()` returns the spare image's size (w, h).

  * `setsparepicturesize(w, h)` sets the spare picture size. All layers are clipped accordingly. If you have made changes on the picture, **you don't need to call finalizepicture()** first, this function does it by itself.


### Palette and colors ###
  * `getforecolor()` returns the Foreground pen color (0-255).

  * `getbackcolor()` returns the Background pen color (0-255).

  * `gettranscolor()` returns the picture's transparent color (0-255) for layers and GIF transparency.

  * `setforecolor(c)` sets the Foreground pen color (0-255).

  * `setbackcolor(c)` sets the Background pen color (0-255).

  * `setcolor(c,r,g,b)` set color index c in palette to (r,g,b)

  * `getcolor(c)` returns the (r, g, b) value of color at index c.

  * `matchcolor(r,g,b)` return the index of the nearest color available in the palette.
  * `matchcolor2(r,g,b)` return the index of the nearest color available in the palette.

  * `getbackupcolor(c)` returns the (r, g, b) value of color at index c, from the original palette (before any changes done by your script).

  * `getsparecolor(c)` returns the (r, g, b) value of color at index c, from the spare's palette.

  * `getsparetranscolor()` returns the spare picture's transparent color (0-255) for layers and GIF transparency.

All of r,g,b and c are normally in the range 0 to 255. For c, if you provide a number outside of this range, it will roll over : for example 300 becomes 45 and -2 becomes 254. Color components r,g and b, however, are clipped to the lower or upper limit.

You can get infos on the palette for selecting your colors when drawing, or you can create scripts that just build a full palette from 2 or 3 colors.

### Windows ###

  * `inputbox(window_title,label_1,initial_value_1,min_1,max_1,digits_1,...)` Opens a window that asks the user for one or several setting values. The control only accepts values between the min and max that you provide, and you can specify how many decimal places of precision it should have with `digits`. You can ask for more than one value by adding arguments: label\_2, initial\_value\_2, min\_2, max\_2, digits\_2 etc, with a limit of 9 settings. This function returns one value to tell if the user accepted or cancelled (true or false), and one additional return value by setting. Example:
```
ok, w, h = inputbox("Modify brush size",
  "Width",     w, 1,100,0,
  "Height",    h, 1,100,0
);
```
    * If min and max are 0 and 1, and digits is 0, it will show a checkbox. Ex:
```
ok, xflip, yflip = inputbox("Transformation",
  "X-Flip",    0, 0, 1,0,
  "Y-Flip",    0, 0, 1,0
);
```
    * If min and max are 0 and 1, and digits is negative, it will show a radio button. Radio buttons with the same number of "digits" are grouped together. Ex:
```
ok, a, b ,c, d = inputbox("Your choice",
  "A",    1, 0, 1,-1,
  "B",    0, 0, 1,-1,
  "C",    0, 0, 1,-1,
  "D",    0, 0, 1,-1
);
```
    * If min and max are 0, the entry is just a label, the user can't input anything on this line.

  * `selectbox(caption,label_1,callback_1,label_2,callback_2)` Opens a window where the user has to click on one of the buttons. You provide the button labels, and Grafx2 executes the associated callback, which must be a function : a pre-defined function (don't type the parentheses after function name) or an anonymous function that you build on the spot. The user can press Esc to cancel. Example:
```
selectbox("Menu",
  "Sub-menu 1", sub_menu1_func,
  "Sub-menu 2", sub_menu2_func,
  "Say hello", function() messagebox("Hello"); end
);
```
  * `messagebox(message)` or `messagebox(window_title,message)` Displays a multiline message. It performs word-wrapping automatically, but you can also include character \n in message to force some carriage-returns. If you need variables in the message, use Lua's concatenation operator .. (two dots) to assemble the message string.

### Interactivity ###

  * `wait(t)` Forces a delay, in seconds (floating values are accepted, rounded to 0.01s). During this time, mouse can move, and if color cycling is active, you'll see it updated. If you use a delay of zero, the program only updates the mouse position and immediately continues. For safety, you can't request a delay of more than 10 seconds.

  * `waitbreak(t)` Forces a delay, in seconds. Similar to `wait()`, except that it returns early with a value of 1 if the user presses ESC, otherwise 0 when the wait is over. `waitbreak(0)` is very useful, it will only update mouse position (and color cycling if it's active) and return 1 if ESC has been pressed since last call.

  * `moved, key, mx, my, mb = waitinput(t)` Waits for user input. _moved_ is 1 if the mouse cursor moved, _key_ is set when the user pressed a key, _mx_ and _my_ are the upadated mouse coordinates, and _mb_ is the mouse buttons state, ie 1 while left mouse button is pressed, and 2 while right mouse button is pressed.

  * `updatescreen()` Redraws the picture on the screen.

  * `statusmessage(message)` Prints the given message in the status bar. Use this when your script is doing long calculations, so the user knows what is going on. Note the message is reset by waitbreak(), so usually you have to display it again before each call to updatescreen.

### Others ###

  * `finalizepicture()` ends your modifications in picture history. The current state of the image (and palette) becomes the "backup", for all functions that read backup state. This can be called multiple times in a script, but remember the history size may be limited. Don't use all of it.

  * `(name, path) = getfilename()` returns the picture name and the path where it is saved. This is useful for saving data related to the picture near to it, and finding it back later (or exporting it for other uses)

  * `selectlayer(1)` select the layer or anim frame to use for pixel access in the main page. If the layer doesn't exist, it throws an error. There is no way to create a layer yet.

  * `run(scriptname)` calls another script. This is a lot like Lua's built-in `dofile()`, but supports directories, and especially relative paths: The called script will update its current directory before running, and pop back to the original script's directory afterwards. The path uses a common format for all OSes: ".." is understood as the parent directory, and "/" acts a directory separator. This will help write scripts that run equally well on Linux, Windows, and Amiga-based OSes.
```
run("../libs/dawnbringer_lib.lua")
```

# Sample script #

Here is a very small sample script that generate a diagonal gradient.

```
-- get the size of the brush
w, h = getbrushsize()

-- Iterate over each pixel
for x = 0, w - 1, 1 do
	for y = 0, h - 1, 1 do
		-- Send the color for this pixel
		putbrushpixel(x, y, (x+y)%256);
	end
end
```

# Known bugs and limitations #
  * The inputbox is limited. If you have needs that it can't meet, please contact us, we'll see if there is a way to improve it.

# More reading #
Lua is a well known programming language.
Here are some pages from the internet you may want to look at for more information :
  * http://lua-users.org/wiki/MathLibraryTutorial Stuff about math.
  * http://lua-users.org/wiki/LuaDirectory The Lua wiki with a lot of pointers to informations.
  * http://code.google.com/p/grafx2/source/browse/#svn/trunk/share/grafx2/scripts The subversion holds a set of scripts you may use as a base for yours. You can send us your scripts if you want them to be added to the list.

# Additional stuff #

It is possible to extend the lua functions with your own ones. There are some examples on how to do that in the 'libs' directory in the link mentioned above.

So far this includes :
  * Memory.lua : persistent on-disk storage for your scripts. Use this for storing your own settings or other data.

We welcome any additions you want to make to this set of functions. If something proves too slow when done in lua, we may provide a faster C version, with the same interface whenever possible. This way all scripts can share the enhancements.