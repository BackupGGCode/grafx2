# HISTORY of GRAFX #
(in reverse chronological order: latest version at the beginning)
## GRAFX 2.4.2035 bugfix release (19/10/2012) ##
  * Palette changes that modify the pixels can't be undone ([issue 514](https://code.google.com/p/grafx2/issues/detail?id=514))
  * Opening a 24bit image in command-line gives wrong mouse cursor ([issue 515](https://code.google.com/p/grafx2/issues/detail?id=515))
  * On some non-x86 platforms, some changes can't be undone on animations > 32 frames ([issue 516](https://code.google.com/p/grafx2/issues/detail?id=516))
## GRAFX 2.4 (01/10/2012) ##
svn revision: [r2024](https://code.google.com/p/grafx2/source/detail?r=2024)
### Improvements ###
  * Support for animation : load, edit and save animated GIFs. ([issue 31](https://code.google.com/p/grafx2/issues/detail?id=31))
  * Tilemap effect ([issue 195](https://code.google.com/p/grafx2/issues/detail?id=195))
  * Mouse panning when holding 'space' key by default ([issue 233](https://code.google.com/p/grafx2/issues/detail?id=233))
  * Preview layers when the image has several layers and you hover the layer buttons
  * Support for saving actual LBM files for Deluxe Paint 3. The previous format is renamed to PBM. ([issue 505](https://code.google.com/p/grafx2/issues/detail?id=505))
  * Improved brush rotation using rotsprite algorithm ([r1789](https://code.google.com/p/grafx2/source/detail?r=1789))
  * Lua bindings: matchcolor2(), getfilename(), run()...
  * Saving a layered image or animation in non-GIF format now prompts the user to save flattened copy or current layer/frame.
  * Can paste text in any text field (from system clipboard. not available on all OSes at the moment)
  * Palette reduction: use DawnBringer's improved color selection
  * Grid size limit is now 999\*999 (up from 80x80)
  * Improved the color reduction algorithm. New one also consumes less memory and has 24 bits of precision instead of 19
  * Skins window: font preview ([issue 450](https://code.google.com/p/grafx2/issues/detail?id=450))
  * Flood-fill icon now has a specific mouse cursor, ([issue 457](https://code.google.com/p/grafx2/issues/detail?id=457)).
  * Add XOR-line helper when drawing circles and ellipses
  * Can load RIFF palette file format
  * Lua script selector displays current directory
  * Support for Lua 5.2
  * Specialized editing mode for Amstrad CPC Mode 5 (In Effect menu: 8-bit)
  * C64 file formats
  * Virtual keyboard can be enabled on all platforms, useful for Tablet PCs ([issue 453](https://code.google.com/p/grafx2/issues/detail?id=453))
  * Right 'Windows' key can be used as a keyboard modifier for shortcuts, unless reserved by your OS.
### Fixes ###
  * Fix crash when browsing drives that have no 'parent directory' entry ([issue 477](https://code.google.com/p/grafx2/issues/detail?id=477))
  * Fix crash when loading 24bit images as brushes
  * Crash when activating magnifier while hovering layer bar ([Issue 480](https://code.google.com/p/grafx2/issues/detail?id=480))
  * Fix a crash that happened in Palette screen when right-clicking near top of screen ([r1938](https://code.google.com/p/grafx2/source/detail?r=1938))
  * Fix a memory corruption in Lua's 'setpicturesize' when using multi-layered images.
  * Fix an error when loading layered image that used a transparent color different from zero ,which resulted in corrupted image.
  * Fix disappearing cursor when using brush rotation tool ([issue 473](https://code.google.com/p/grafx2/issues/detail?id=473))
  * Resizing not precise enough on small pictures/brushes ([issue 435](https://code.google.com/p/grafx2/issues/detail?id=435))
  * IFF (ilbm/pbm) loading: fix a slight imprecision in loading the palette (last 2 bits of the RGB channels)
  * Default 'load' directory was the program's directory instead of the one from loaded image ([issue 448](https://code.google.com/p/grafx2/issues/detail?id=448))
  * Lasso-ing a brush with right mouse button wouldn't erase cleanly (visual)
  * Inconsistent directories in file selectors for image and brush. ([issue 462](https://code.google.com/p/grafx2/issues/detail?id=462))
  * Fix a graphical mouse bug that happened when toolbar was hidden and you moved the mouse from layer button to image.
  * Loading a GIF animation as a brush now loads first frame, instead of all images piled on each others
  * Previewing a GIF animation now displays first frame instead of all images piled on each others
  * Fileselectors: 'Parent directory' inserts the parent directory string (slash or ..) in filename ([issue 498](https://code.google.com/p/grafx2/issues/detail?id=498))
  * In file selectors, 'parent directory' was sometimes missing in some drives or subdirectories ([issue 506](https://code.google.com/p/grafx2/issues/detail?id=506))
  * After rotating a brush with the 180-degree button, following rotations and flips occurred as if the 180-turn never took place ([issue 460](https://code.google.com/p/grafx2/issues/detail?id=460))
  * Fix a bug in brush distort that often caused the brush to disappear entirely after distort (all color zero)
## GRAFX 2.3.1781 bugfix release (19/04/2011) ##
  * Fixed: Mouse cursor deadzones in fullscreen mode, especially if you change the program's mouse sensitivity ([issue 428](https://code.google.com/p/grafx2/issues/detail?id=428))
  * Fixed: Removed a source of mouse cursor lag while drawing ([issue 269](https://code.google.com/p/grafx2/issues/detail?id=269)), especially on X11, by speeding up the graphic redraw.
## GRAFX 2.3.1778 bugfix release (16/04/2011) ##
  * Fixed: Graphical glitch in Options screen ([issue 432](https://code.google.com/p/grafx2/issues/detail?id=432))
  * Fixed: Menu colors changed on reload, causing very often the cursir lines to be black over black ([issue 433](https://code.google.com/p/grafx2/issues/detail?id=433))
## GRAFX 2.3 final (09/04/2011) ##
svn revision: [r1770](https://code.google.com/p/grafx2/source/detail?r=1770)
### Improvements ###
  * Added 2 virtual keyboards for portable console ports - one to easily enter filenames or text for text tool, another one for all numeric input.
  * Magnifier settings for Main page and Spare page are now synchronized, if the images have same dimensions ([issue 327](https://code.google.com/p/grafx2/issues/detail?id=327))
  * Many new Lua functions for scripting
  * Lua scripts can now be located anywhere on your disk (the window allos browsing).
  * Improved the color matching formula used in 'Copy to Spare' and 'Recolorize brush'
  * Rotating a brush while holding 'Shift' key now snaps to the closest 22.5° multiple)
  * Added color cycling animation ([issue 365](https://code.google.com/p/grafx2/issues/detail?id=365)). Animation can be active even when drawing.
  * Color cycles (or gradients) are now saved in PNG and GIF formats.
  * Paintbrush window can be customized with your own brushes ([issue 345](https://code.google.com/p/grafx2/issues/detail?id=345)). It also highlights the selected one.
  * The colorpicker cursor, (in zoomed view) no longer displays a preview pixel.
  * Fixed the bottom line of pixels in the magnifier: The bottom row can no longer be too thin.
  * Redesigned Settings window. Now contains all settings that were only available in gfx2.ini
  * Safety backups (after a crash or power failure) now remember the original file name and directory.
  * File sorting in file selector is case insensitive
  * New drawing workflow allowing to use right click as a colorpicker instead of drawing with the secondary color where it makes sense
  * Allow skins to redefine the "selected" button graphics
  * Real alpha transparent mode. Allows to properly use antialiased-text on a multicolor background
  * Copy and paste in the palette using ctrl C/ctrl V or right-click sub-menu.
  * Cleanup of the palette screen and added a way to input colors in hexadecimal.
  * Palette screen : Added a button to tag used colors
  * Palette screen : Added a color histogram
  * Palette screen : Reducing color count now removes duplicates
  * Palette screen : Added a merge tool
  * New shortcuts for brush resize and calling factory scripts directly
  * New algorithm for palette sorting
  * Support fonts in 'bitmap Font Writer' format.
  * Drag-and-dropping a file into Grafx2's window now opens it.
  * Drive list (in Load/Save screen) now has icons for media type: HDD, CD, etc.
  * Allow saving XPM images
  * Hold Control and Click to perform a right-click : handy for tablets and similar devices. An option allows you to pick different keys ([issue 400](https://code.google.com/p/grafx2/issues/detail?id=400))
  * Text tool : With bitmap fonts, you can now enter carriage returns using Alt+Enter
### Fixes ###
  * Keyboard shortcuts are now exclusive by default (you can change option if needed). This avoids the need to unset a shortcut when you need the key for something else.
  * Fixes aevere image corruption when scrolling image while some layers are hidden ([issue 417](https://code.google.com/p/grafx2/issues/detail?id=417)).
  * Palette screen: Undo is now much more reliable ([issue 354](https://code.google.com/p/grafx2/issues/detail?id=354))
  * Better control of brush palette ([issue 362](https://code.google.com/p/grafx2/issues/detail?id=362))
  * Text tool with bitmap font now works much better with colored fonts, especially if you use 'Get brush colors'.
  * Fix the Saturation slider in HSL mode that would make greyscale colors red ([issue 396](https://code.google.com/p/grafx2/issues/detail?id=396))
  * Menu size (depending on UI scale) doesn't change when Pixel Scaler changes, when it's possible ([issue 338](https://code.google.com/p/grafx2/issues/detail?id=338))
  * Fix a bug where closing the Magnifier moved the view to random place ([issue 380](https://code.google.com/p/grafx2/issues/detail?id=380))
  * Lua : too many fixes to list
  * Fix important bug where resizing an image or using any transformation resets transparent color to zero
  * Fix imprecise RGB sliders when RGB scale is lower than 256 ([issue 384](https://code.google.com/p/grafx2/issues/detail?id=384))
  * Skin DPaint: Fix the icon 'unslected layer 6'
  * Skin DPaint: Fixed the hotspot of the standard mouse cursor, it was not in top left corner.
  * Skin Modern: Fix the button for palette scroll arrows
  * The image preview in Load/Save window now uses a web-safe palette, if the previewed image has a low color count.
  * Fixed the 'Copy to Spare / palette and remap' : It wasn't fully undoable.
  * Improved mouse handling. Should fix many cases mouse cursor was choppy or lagging for no reason, taking lots of CPU.
  * Modified the method for picking GUI colors in the current palette. This solves many cases where the menu was difficult to read.
  * Fix using fullscreen mode with a tablet ([issue 317](https://code.google.com/p/grafx2/issues/detail?id=317)).
  * Fixed the format of gfx2.ini, which was sometimes causing the loss of the "scroll up" shortcut.
  * Fixed a few typos in Keyboard Shortcuts help.
  * Fixed crash on loading PNG24 pictures if they contain transparency data.
  * Fixed inaccurate picking of color in the menu palette and improved its ergonomy ([issue 340](https://code.google.com/p/grafx2/issues/detail?id=340))
  * The gradient rectangle tool can no longer leave construction lines ([issue 339](https://code.google.com/p/grafx2/issues/detail?id=339))
  * Fixed the "Zap unused colors" funtion, in some cases it would affect wrong colors.
  * Fixed compilation problem for Linux ([Issue 336](https://code.google.com/p/grafx2/issues/detail?id=336))
  * F1 key in settings screen didn't open the right help files
  * Better compatibility in the GIF file loader (1bpp GIFs and other things)
  * Trying to use a font bigger than 99 and some bitmap fileformats would crash the program
  * Keyboard click emulation was broken since 2.1

## GRAFX 2.2.1430 bugfix release (27/03/2010) ##
  * Fixed Text window which never closes when opened by 'T' ([Issue 333](https://code.google.com/p/grafx2/issues/detail?id=333))

## GRAFX 2.2 final (22/03/2010) - Dragon's Layers Edition ##
### New features ###
  * Layers
  * Lua binding to generate and alter picture and brush with scripts
  * Two new skins by Jamon and iLKke
  * GIF and PNG transparency
  * Shortcut keys can be bound to multiple actions
  * Load more image formats when SDL\_image can handle them (jpeg, tga, ...)
  * Show number of pixels used by colors in the selected range in palette window
  * Preview skins in the skin dialog. Move more settings there. Load prefered menu colors from the skin. Fix changing to a screen that use different color indexes for its menu colors
  * Save Amstrad CPC pictures in .SCR format.
  * Menu toolbars can be separately shown or hidden
  * Safety backups are made automatically about every minute, and reloaded after a crash or program halt
### Improvements ###
  * Zoom-on-mouse, also when changing the zoom factor
  * More zoom levels are available for the magnifier (up to x32)
  * Help message when running in console with /? or similar switch show some more options and a readable list of fullscreen modes
  * Only show recognized file extensions and not all files by default in save/load screen
  * Shade window selects the foreground color by default when opened, and if you close it with only one color selected either in the palette or the range filer, this color is selected as foreground
  * Added more space for filename in status bar
  * Better command line handling, allowing more options and possibility to load an image for the spare page too
  * Menu zoom is now maximum x2 by default. Avoids having a really big menu on modern screens
  * Rewrite of the save and load system to avoid a risk of corrupting the picture in some special cases
  * Program remembers the pixel scaler you used last
### Fixes ###
  * Fix a possible crash when using grad rectangle with shift key
  * Load and save palettes in "jasc" format and with the full 0..255 range
  * Removed deprecated setting "mouse correction factor"
  * Reset quicksearch when entering a directory in load/save dialog
  * Rotating a brush 180° was broken if the height was even since [r763](https://code.google.com/p/grafx2/source/detail?r=763)
  * Fix BMP saving again
  * Help page for Contour fill had a line too long
  * Fix potential endianness and packing problem in all file formats.
  * The homepage address on the splash screen was wrong !
  * Crash if you enable mask with 2 pictures of different size in main and spare
  * Mask and Stencil shortcuts were reversed in the FX window
  * Joystick is now disabled by default to avoid mouse drifting
  * Text tool: Bitmap fonts painted in "color 0" now work
  * Fix a wrong shortcut (filled circle) in helpscreen
  * Fix the loading of some C64 format files

## GRAFX 2.1.1080 bugfix release (20/09/2009) ##
  * Fixed: High CPU usage even when the program is idle ([issue 217](https://code.google.com/p/grafx2/issues/detail?id=217)).

## GRAFX 2.1 (13/09/2009) ##
  * New: C64 file formats ([Issue 211](https://code.google.com/p/grafx2/issues/detail?id=211)).
  * Fixed: Crash with gradient-filled rectangle ([Issue 212](https://code.google.com/p/grafx2/issues/detail?id=212)).
  * New: Visible tile grid in zoomed view (alt-shift-G).
  * Fixed: Moving a very large brush in zoomed view would not refresh fast enough ([Issue 183](https://code.google.com/p/grafx2/issues/detail?id=183))
  * Improved: Resizable "circle" paintbrush now proposes all diameters, no longer limited to odd ones.
  * Improved: Resizable "random" paintbrush has a more even flow.
  * New: Brush container, in Paintbrush screen. Store and retrieve up to 12 brushes.
  * Improved: Slow operations (ex: circle with big brush and Transparency active) now draws some intermediate steps ([Issue 183](https://code.google.com/p/grafx2/issues/detail?id=183))
  * Changed: Color reduction when loading 24-bit BMP PCX or PNG no longer applies Floyd-Steinberg dithering. It picks nearest match instead.
  * Fixed: greyscale PNG loading.
  * Improved: PNG 24-bit can now be loaded, with color reduction ([Issue 201](https://code.google.com/p/grafx2/issues/detail?id=201)).
  * New: Keyboard shortcuts for assigning fixed zoom levels.
  * Improved: Palette screen remembers if you prefer HSV or RGB.
  * Fixed: Possible crash in Save/Load screen if directory content was modified ([Issue 198](https://code.google.com/p/grafx2/issues/detail?id=198))
  * Improved: You can exit text fields by clicking elsewhere.
  * Improved: You can now choose a fixed GUI scaling factor ([Issue 101](https://code.google.com/p/grafx2/issues/detail?id=101))
  * New: Hold SHIFT while drawing a line finds the closest multiple of 45° or isometric angle.
  * New: Hold SHIFT while using any other tool to lock X or Y axis ([Issue 193](https://code.google.com/p/grafx2/issues/detail?id=193))
  * Fixed: Dragging sliders and clicking color color ranges no longer activate other parts of windows ([Issue 191](https://code.google.com/p/grafx2/issues/detail?id=191))
  * Key-combo support to quickly set transparency, ie you can type 3 4 to get 34% transparency ([Issue 154](https://code.google.com/p/grafx2/issues/detail?id=154))
  * New keyboard shortcut: All effects off (shift-E)
  * Gradient-filled rectangle and Gradient menu are now a single button.
  * New settings screen specifically for the look of the program (font, menu graphics, mouse cursor) : Right-click the Settings button.
  * New default skin and several alternate fonts, made by Ilkke.
  * Fixed: Releasing shift control or alt had the extra effect of releasing all mouse buttons ([issue 187](https://code.google.com/p/grafx2/issues/detail?id=187))
  * Improved: MacOSX : Configuration is now preserved when upgrading grafx2 ([issue 192](https://code.google.com/p/grafx2/issues/detail?id=192))
  * New: Support for loading and saving Neochrome image file format (.NEO files)

There was some bugs left in the first 2.0 release, so we fixed them while working on new features for 2.1. These versions only include the bugfixes, and not the new features. 2.0 will be supported like that until we get 2.1 out.

## GRAFX 2.00.970 bugfix release (08/06/2009) ##
  * Fixed: Crash in Load/Save dialog when directory content has changed. ([issue 198](https://code.google.com/p/grafx2/issues/detail?id=198))

## GRAFX 2.00.951 bugfix release (07/24/2009) ##
  * Fixed: Crash when using pipette on a software-zoomed video mode from the palette screen ([issue 196](https://code.google.com/p/grafx2/issues/detail?id=196))

## GRAFX 2.00.880 bugfix release (20/06/2009) ##
  * Fixed: 'Out of memory' message on machines with more than 4Gb free RAM ([issue 182](https://code.google.com/p/grafx2/issues/detail?id=182))

## GRAFX 2.00.874 bugfix release (16/06/2009) ##
  * Fixed: Quicksearch filenames and brush resize shortcuts don't work ([issue 180](https://code.google.com/p/grafx2/issues/detail?id=180))

## GRAFX 2.00 final (06/12/2009) - Summer Sunset Edition ##
This is the final GraFX 2.0 release. It includes everything planned by sunset design, and some more.
  * Fixed: A delay on window resize ([issue 169](https://code.google.com/p/grafx2/issues/detail?id=169))
  * Fixed: Display of filenames in Save/Load, when they contain multiple dots ([issue 170](https://code.google.com/p/grafx2/issues/detail?id=170)).
  * Improved: Added user-definable mouse sensitivity, useful for fullscreen low-res modes ([issue 159](https://code.google.com/p/grafx2/issues/detail?id=159)).
  * Fixed: (Linux) The window "resisted" resizing ([issue 161](https://code.google.com/p/grafx2/issues/detail?id=161))
  * Fixed: (Win98) Crash related to key ^ on French or German character ([issue 167](https://code.google.com/p/grafx2/issues/detail?id=167))
  * Fixed: Bookmarks didn't allow characters ; and # in their name or target ([issue 166](https://code.google.com/p/grafx2/issues/detail?id=166)).
  * Improved: (Windows) The program records window position on exit, and restores it on startup.
  * Fixed: Some odd keys were displayed with the wrong scancode in help and config.
  * Improved: Added buttons x2 and /2 to select usual color scales easily.
  * Improved: Allows "2" as RGB scale.
  * Improved: Made RGB scaler a bit larger in palette secondary screen.
  * Fixed: Preview in text window is now drawn with the back color, so you can see the antialiasing correctly.
  * New: Allow sorting only a range of colors in the palette : when you right-click 'Sort'.
  * Fixed: Reverted Lightness sorting order so white is first.
  * Fixed: colorpicker cursor disappearing when too close to screen edge
  * New: Picture effects screen : Resizes / mirrors / rotates image
  * New: Distort brush ([Issue 34](https://code.google.com/p/grafx2/issues/detail?id=34))
  * New: Pixel scaler "Triple" for 3x3 zoom ([Issue 147](https://code.google.com/p/grafx2/issues/detail?id=147))
  * New: Pixel scaler "Quadruple" for 4x4 zoom ([Issue 151](https://code.google.com/p/grafx2/issues/detail?id=151))
  * New: Pixel scaler "Wide2" for 4x2 zoom ([Issue 148](https://code.google.com/p/grafx2/issues/detail?id=148))
  * New: Pixel scaler "Tall2" for 2x4 zoom ([Issue 149](https://code.google.com/p/grafx2/issues/detail?id=149))
  * Fixed: Resizing the image didn't mark the image 'modified since last save'
  * Fixed: When drawing a gradient ellipse, the cursor remained on screen after the drawing operation.
  * Fixed: Grafx2 now works on SPARC cpu
  * Fixed: Some specific macosx shortcuts (command+h)
  * Improved: You can assign "command"+key shortcuts, if the combination isn't a system one.
  * Improved: Discontinuous freehand now uses an asynchronous method for delaying. It is sensitive to the delay set in the airbrush/spray menu.
  * New: Frame the backcolor with a dark dotted line.
  * New: Double clicking in palette will open the palette window.
  * Fixed: Made the "Safe resolution" shortcut do nothing in windowed mode. ([issue 118](https://code.google.com/p/grafx2/issues/detail?id=118))
  * New: Shortcuts for previous and next colors in user-defined range. (Keys = and -) They use the Shade settings.
  * Fixed: In Shortcuts screen, explanation text can no longer overdraw the border.
  * Fixed: Grey out + and - buttons in palette screen when you use HSL mode, as they are irrelevant this mode.
  * Fixed: Removed useless precalculation tables that made the program crash on very high resolutions
  * Fixed: Big ellipses had an overflow in claculations
  * Fixed: Help screens updated
  * Fixed: Clear values of some text fields on right click
  * Fixed: mouse shortcuts were not locked in some cases, causing screen corruption
  * Fixed: GP2X build use correct 320x240 size by default, and no longer proposes a windowed mode. Write confing on the local dir and not $HOME.
  * Fixed: when there are less than 12 modes it was possible to cause a segfault when opening the screenmodes list.
  * Fixed: source archives are now packed with a directory inside, the usual unix way.

## GRAFX 2.00 Beta 99.0% (04/13/2009) ##
Much more stable than beta 98.0%.
  * Improved : Grafx2's default FG and BG colors are now white and black (instead of 15 and 0).
  * Fixed : Palette ordering ([issue 112](https://code.google.com/p/grafx2/issues/detail?id=112)). You can activate it in the secondary palette window (shift-P), it's saved in gfx2.ini.
  * Updated : contextual help for all the new tools and features.
  * Fixed : display of mount points and drives ("Select drive" button) in Load/Save
  * Improved : Cleaned up the layout of Save/Load screen. ([issue 92](https://code.google.com/p/grafx2/issues/detail?id=92), [issue 84](https://code.google.com/p/grafx2/issues/detail?id=84)#4)
  * Fixed font selection, was off by 2 pixels (Text tool)
  * Improved : Menus: scrollbars are now dark.
  * Improved : Codesource is now written in english. Patches welcome.
  * Removed : Open Watcom support.
  * Removed : gfx2cfg tool, we don't need it anymore.
  * Fixed : small BMP files saving
  * Fixed : [issue 129](https://code.google.com/p/grafx2/issues/detail?id=129) : polyform unusable when effects are active
  * Improved : Tidied up the splash screen (can no longer drag it)
  * Fixed : the quick-typing that wasn't reset when changing directories in save/load
  * Fixed : a missing refresh on first click of tools: lines, curves, polygon, grad circle/ellipse
  * Fixed : Forbid resolutions < 320x200 ([issue 126](https://code.google.com/p/grafx2/issues/detail?id=126))
  * Added : Bookmarks ([issue 92](https://code.google.com/p/grafx2/issues/detail?id=92)) in Save/Load screens
  * Fixed : Resolution changes: No longer reset the mouse cursor in center of screen.
  * Fixed : Sieve menu display with tall/wide pixels or large resolution
  * Improved : Dropdown lists in Save/Load for choosing file format.
  * Fixed : [issue 122](https://code.google.com/p/grafx2/issues/detail?id=122): Qshade only working in one direction with some tools.
  * Fixed : the pipette leaking drops ([issue 115](https://code.google.com/p/grafx2/issues/detail?id=115)) and a few other display bugs on mouse click or release
  * Added : Double Pixel mode ([issue 86](https://code.google.com/p/grafx2/issues/detail?id=86)) Tall pixels can now be used in resolution minimum 320x400, and Tall pixels minimum 640x200. (instead of 640x400 for both)
  * Fixed : There was incorrect error recovery when trying to use a fullscreen mode too small to use wide/tall/double pixel.
  * Fixed : GrafX2 can be used on ...DOS with HX extender.
  * Fixed : Do not crash if there is more than 4GB memory available.
  * Added : Last-chance recovery that saves the current and spare page on crash. ([issue 97](https://code.google.com/p/grafx2/issues/detail?id=97))
  * Fixed : an old, possibly lethal memory overrun in Backup buffers, when using long file names (>12)
  * Fixed : Palette screen: Copy,Swap,X-Swap now take place when you click button, not release. In all screens where you could press ````` and pick a color (palette, shade...): The action now takes place when you click, not release.
  * Added : The secondary Palette screen (right-click [PAL](PAL.md) or press shift-P) now allows changing the menu palette cells, as well as the RGB scale.
  * Improved : Grad Rect cancellation now works
  * Fixed : In gfx2.ini, setting Merge\_movement to >0 should help solve lag ([issue 80](https://code.google.com/p/grafx2/issues/detail?id=80)) for users who have a mouse with update frequency >100Hz
  * Fixed : refresh problem when rotating a brush outside of screen limits (bug in 98%)
  * Fixed : Palette window having 'S' as shortcut for 2 functions.
  * Fixed : When you use a keyboard shortcut to activate a window button (ex: ESC), it shows it's activated.
  * Added : Keyboard shortcuts are customizable from within Grafx2. 2 shortcuts per function. You can use keys, MouseWheel, Middlebutton, joystick buttons, in combination with Alt, Shift, Control.
  * Added : Safety in Help text GUI image change: Added more characters in help font.
  * Fixed : monochrome image preview (add some sane colors). Real 2-color palette is still used on loading the picture.
  * Fixed the missing confirmation message ([issue 105](https://code.google.com/p/grafx2/issues/detail?id=105)) in save/load
  * Added : 'repeatable buttons' that work like slider arrows : [+] [-] in Palette and Text, and for the arrow buttons that scroll Sieve pattern.
  * Improved : Buttons: Now you can 'cancel' a click by dragging the mouse outside of the button before releasing click, pretty much like a Windows button.
  * Fixed : buttons being depressed on mouse press
  * Fixed : missing refresh on color select with keyboard shortcut
  * Fixed : CRASH in Help screen, when pressing PageDown in pages of less than 16 lines.
  * Fixed : the double icons having their diagonal not shaded on selection. Fixed the Ellipse / Grad ellipse icon graphics (were quite off-centered)
  * Added : Contour fill, 4th mode of continuous drawing. (deluxepaint-like)
  * Added : PNG file format load and save
  * Fixed : the characters in Smooth window (shift-F8) and the string-editing cursor, both were drawn rotated 90degrees :)
  * Fixed : the close button requiring an extra click somewhere (on win9x at least)
  * Fixed : Some cleanups to the "credits" help page, as it felt a little bit messy.
  * Added : FreeBSD version available
  * Fixed : Default filename is now in .gif instead of .pkm
  * Improved : gfx2.dat is now replaced by an editable "skin" file (gif format). Two skins available : classic and modern done by Ilkse
  * Added : (un)installer script for windows (NSIS).
  * Fixed : When the last resize was by the 'safe resolution' button, on exit the program recorded the previous window size instead.
  * Fixed : "Parent dir" in the file selector for amigas. Should make it easier to use.
  * Fixed : Rotating a very small brush does not crash the program anymore.

## GRAFX 2.00 Beta 98.0% (01/??/2009) ##
  * Added : palette constraint modes: Run the program with command-line option "/rgb `<N>`" to force RGB components have N levels instead of 256. Ex: /rgb 16 enforces a classic Amiga 4096 color palette, 64 is PC VGA, /rgb 3 is Amstrad CPC...) Added missing messages for /wide and /tall command-line arguments.
  * Improved : Use GIF as the default format, as PKM can't save the whole palette range.
  * Imroved : The buttons in the screens FX and Brush FX now use the same shortcuts as when drawing.
  * Fixed : The Spray tool no longer lags when you use a >0 delay setting. Delay is now expressed in 1/100s, with range 0-99
  * Fixed : a severe memory leak, up to 200Kb every time you closed a window.
  * Added : Simple joystick support.
  * Added : a listing of all the mountpoints under linux.
  * fixed : Sliders no longer lag the mouse cursor, and the delay stops when you release one mouse button or click the other.
  * Fixed : Endianess in Save\_BMP
  * Fixed : screen updates problems
  * Fixed : keyboard-drawing in zoom area: "Escaping" the zoom window, and going up at the top warps to the bottom. Also, even with mouse,when you draw downwards into the menu, the cursor no longer blinks into the top line of the menu.
  * Improved : Cursor moves faster when using the keyboard shortcuts over the zoomed screen.
  * Fixed : some problems of sreen update in smear mode ([issue 66](https://code.google.com/p/grafx2/issues/detail?id=66)) and possibly some others.
  * Fixed : a bug which attempted to refresh below the screen when menu is hidden
  * Fixed : Random crash and weird coordinates of viewports when resizing the screen (w/ and w/o zoom, with resolution change or window resize)
  * Fixed : crash when using line,polyline,polygon etc. with a starting point below the picture (outside).
  * Fixed : [issue 56](https://code.google.com/p/grafx2/issues/detail?id=56): Window resizing and zoom mode.
  * Fixed : [issue 70](https://code.google.com/p/grafx2/issues/detail?id=70): Keyboard shortcuts during brush rotation and stretch.
  * Improved : Allow sliders to scroll more than once when the mouse button is pressed
  * Fixed : broken characters >127 in the help window. Fix broken characters >127 in normal fonts.
  * Remove : useless setting "show system directories".
  * Fixed : wrong color selection in Spray menu when clicking between columnns
  * Added : Support for "wide pixel" mode (Each pixel is 2x1). Run the program with "/wide" argument to test. Now you can draw graphics for Amstrad CPC's "mode 0" :)
  * Improved : Now idles when there is nothing to do. Much less CPUtime use, but the spray is slowed down.
  * Added : Support for "tall pixel" mode (Each pixel is 1x2). Run the program with "/tall" argument to test. The following tools don't take the ratio into account; Circle, Grad rectangle, Brush rotation, Resizable brushes (diamond, squares, circles...)
  * Improved : faster color reduction algorithm.
  * Fixed : "Backspace" shortcut detecting root only on MS filesystems in load/save screen.
  * Improved : On all screens that display a palette, the grey columns are no longer "dead", you can click them to pick the color to its right.
  * Fixed : display of colored rectangles in Palette screen ([issue 64](https://code.google.com/p/grafx2/issues/detail?id=64))
  * Fixed : wrong shortcuts in Palette screen Removed an obsolete message ("Sensibilite Souris") and dead code
  * Fixed : Floyd steinberg dithering. The error was added to the neighbour pixels, it is now substracted, the results are much better. However, the palette seems to lack saturated colors (in comparison to the one generated by gimp, wich gives more dithering, but better overall subjective ressemblance to the 24bit image.
  * Improved : Palette now uses RGB components in the full 0-255 range instead of 0-63. All palette functions can be used in HSL color space too.
  * Improved : directory handling: - Unix users can "make install" and "make uninstall" (as root). - Installation creates shortcuts "grafx2" and "gfx2cfg" in /usr/local/bin - Installation puts data files (icon GIFs, gfx2.dat,..) and the actual binaries in /usr/local/share/grafx2 - At runtime, the programs search and create configuration files (gfx2.cfg and gfx2.ini) in ~/.grafx2 (But if there are some present in program's own directory, they override)
  * Fixed : program hang in Save/Load ([Issue 59](https://code.google.com/p/grafx2/issues/detail?id=59))
  * Improved : Add 32 null bytes at end of PI1 files to make ST Deluxe Paint happy
  * Improved : Help screens show the keyboard shortcuts from current configuration
  * Fixed : long filenames, and cursor keys while editing text
  * Added : handling for right mouse button when entering filenames input array (clears it) also using escape key restores old filename.
  * Fixed : Clicking the button with default filename in an empty directory wouldn't work.
  * Fixed : crash in Save\_PKM() which were due to the packing routine accessing a byte of a picture beyond the allocated memory block.
  * Fixed : the display of the current directory size if it is big.
  * Fixed : drawing with the keyboard. Space key release wasn't taken into account. Now you can plot a single pixel.
  * Added : Load/Save: "Select Drive" button. Allows a way for the AmigaOS4 version to display the list of drives / volume names.
  * Added : TEXT Tool with support for truetype and bitmap fonts.
  * Fixed : sprite cursor drawing on screen edges
  * Added : AmigaOS 3, BeOS, Haiku, AROS, SkyOS, MorphOS, gp2x support
  * Fixed : x-swap and swap
  * Added : Gradiation rectangle.
  * Added : support for 192:145 (1152\*870) aspect ratio in screen sizes dialog (and revamped the column a bit).
  * Improved : Straight lines drawn with shift + click.
  * Added : Palette sorting.
  * Fixed : text alignment in the about screen
  * Added : the Additive and Substractive modes, missing from the DOS version
  * Fixed : Implemented Meilleure\_couleur\_sans\_exclusion().

## GRAFX 2.00 Beta 97.0% (10/??/2008) ##
  * Improved : Welcome screen behave like a spash screen: Any click or keypress dismisses it.
  * Added : The SVN revision used to compile is now reported in the Statistics window.
  * Improved : Multiple windows can be open at the same time
  * Added : Contextual help with F1 key
  * Fixed : resolution menu behavior when less than 12 resolutions are available.
  * Removed : useless "vesa info" field in the stats window
  * Added : Resolution and window size remembered in gfx2.ini.
  * Improved : SDL Graphics mode detection and checking if valid, CFG saves only  configuration for valid modes where the user set <3 | Imperfect | Unsupported.
  * Improved : Video modes can now be windowed or fullscreen. Also allows to resize the window at runtime.
  * Imroved : When gfx2.ini is missing, default values are now taken from gfx2.dat.
  * Added : New configuration tool
  * Added : Long file names support
  * Fixed : Use fopen/fread instead of open/read. This is buffered and cross platform.
  * Fixed : Do not crash if there is more than 1GB ram available
  * Fixed : Made the code endian-aware and do not assume structure packing
  * Improved : Rewrote a big part of the program to make it work with SDL under linux, windows, mac os X, and amigaos4. This version will not run directly under good old MS-Dos, but it is still possible to use HX-DOS extender with the windows version.
  * Introduces a lot of new bugs, most notably missing refresh of screen.

## GRAFX 2.00 Beta 96.5% (12/23/1999) - Xmas'99 release ##
  * Fixed: This version seems (is!) stable even with huge pictures. :)
  * Fixed: A few options on brushes kept modifying the continuity of the free-hand drawing mode.
  * Fixed: The "nibble brush" operation crashed sometimes.
  * Fixed: Remapping the screen after modifying colors in the palette editor displayed, in rare cases, unexpected pixels or even crashed. It didn't remap correctly the picture in "Magnify" mode, too.
  * Fixed: Catastrophic bug occuring when you "flood-filled" an area starting at the bottom of the picture.
  * Added: An option in GFX2.INI to tell if the number of colors used must be automatically calculated, and another one for the default video mode at startup.
  * Fixed: The colors of the menu are now correctly remapped when getting colors from the brush.
  * Added: Degas Elite's file formats (PI1,PC1,...) support.
  * Added: True-color BMP (Windows) and PCX images can be loaded. They will be converted to a 256-color image with palette optimization and Floyd/Steinberg dithering. Note: some other true-color formats will be added in the next release.
  * Fixed: Loading corrupt pictures with null dimensions could crash.
  * Improved: Brush streching is now in "real time" (and snaps to the grid if "Adjust brush picking" is set).
  * Added: Brush rotation by any angle.

## GRAFX 2.00 Alpha 96.3% (04/11/1998) - Lucky n' Tigrou Party 2 release ##
!!! Warning: possibly unstable version !!!
  * Improved: You can edit pictures bigger than 1024x768, and small pictures take much less memory, allowing to have many more undo pages!
  * Improved: The list of undo pages is preserved when you load a picture, modify its size, or just go to the spare page.
  * Added: You can "kill" a page (i.e. removing it from the list of undo pages).
  * Modified: The Settings menu has been reorganized.
  * Improved: The drawing mode is no more set to "discontinuous" by default.
  * Improved: The function to compute the best matching RGB color used in smooth, colorize, and some other operations has been strongly accelerated on 486 and Cyrix processors, while it should be about the same speed or very slightly slower on Intel Pentiums (II) than before.
  * Fixed: The program finally works under Windows NT (without dos4gw)!

## GRAFX 2.00 Beta 96.1% (02/28/1998) - Volcanic Party 4 release ##
  * Fixed: File selector gauges don't bug any more when there are more than 584 entries :) in the current directory.
  * Fixed: The file selector _should_ hang no more on non-image (or corrupt image) files containing data that look like a known format signature.
  * Fixed: Old and horrible :) video bug. Most of the VESA video cards that displayed unexpected pixels (when moving the mouse for instance) should work better (perfectly?) now.
  * Fixed: The mouse correction factors didn't work properly.
  * Added: Quick-shade mode.
  * Improved: You can hide any menu that needs a color selection to pick up a color behind the window.
  * Added: A couple of new parameters in the GFX2.INI file.

## GRAFX 2.00 Beta 96% (11/03/1997) - Saturne (aborted) party 5 release ##
  * Added: Now, you can increase or decrease the size of the paintbrush. The default keys are [,<] and [.>] ([;.] and [:/] for azerty).
  * Added: Typing the first letters of a filename in file-selectors will place the selection bar onto it.
  * Fixed: Small but annoying bugs in the writing of the GFX2.CFG file in GFXCFG. The data concerning Shade and Stencil modes were destroyed.
  * Added/Improved: It is now possible to define the matrix of the Smooth mode. We also seized the opportunity to improve the Smooth on the boundaries of the picture, and to improve the function that calculates nearest colors.
  * Added: The "Replace color" option that replaces all the pixels of the color pointed by the mouse with the paintbrush color. This tool is accessible by right clicking on the Floodfill button.
  * Improved: FloodFill slightly accelerated (especially with small surfaces).
  * Fixed: The picture was automatically zoomed when choosing a zoom factor in the menu if the Fast\_zoom option was set.
  * Added: "Stretch brush".
  * Added: Now, you can move windows (menus) and even hide the palette menu for picking a color that is behind it (with the key just below `<Escape>` ).
  * Fixed: Small bug in "Menu\_ratio=2" mode when remapping the screen after color changes.
  * Added: "Thin" cursor type (looks like VGApaint's one).
  * Fixed: A few video modes (Modes X with a height multiple of 224 and some others).
  * Added: It is now possible to select the colors that can be used for the smooth and transparency modes, and remapping.
  * Fixed: Clicking twice on the Lasso button did not restore the paint-brush correctly.
  * Fixed: the absolute coordinates option wasn't correctly saved in the .INI file.
  * Added: A few new parameters can be defined in the .INI file.
  * Added: "Copy palette to spare page and remap destination" option (accessible from the "Copy to spare page" menu (default: Shift+Tab)).

## GRAFX 2.00 Beta 95.5% (09/04/1997) ##
  * Improved: SCx files with less than 256 colors are now supported.
  * Fixed: Bug when double-clicking on the Floodfill button.
  * Fixed: Bug when "flood-filling" with an effect with feedback.
  * Fixed: Bug when filling a vertical-1-pixel-wide area.
  * Fixed: Bug of the shape of the cursor when a window is open in magnify mode.
  * Added: Special cursor shape for the pipette.
  * Modified: The method to recenter the page when exiting magnifier mode (the picture recovers its position as it was before zooming).
  * Added: Linear Frame Buffer (VESA 2.0 LFB) supported.
  * Added: You can now load and save brushes (from the Brush FX menu).
  * Fixed: A few video modes (Modes X with a height multiple of 270).
  * Fixed: You couldn't save the configuration in the settings menu if the Auto-save option was off.
  * Improved: Polyform has now reached its definitive behaviour.
  * Added: Polyfill and filled polyform.
  * Added: Lasso (polyformed brushes).
  * Added: Concentric lines.
  * Added: GFX2.INI file (check its contents for new options).
  * Improved: GFX2.CFG file will have ascending compatibility with future versions from now.
  * Added: Some drawing tips have been detailed in the documentation files.
  * Improved: Pipette handling.

## GRAFX 2.00 Beta 95% (07/18/1997) - Wired'97 release ##
(It's GrafX2 creation's 1st anniversary! =D     (...but still Beta :/) We wrote the usual "void main(int argc, char `*` argv[.md](.md))" one year ago!)
  * Fixed: PCX files with odd widths should be supported now. (We fixed a bug in version 94.1% which added a new one) :(
  * Fixed: Small display bug in the grid of the Sieve menu.
  * Fixed: Oops! We forgot to remap the colors of the menu when loading a PAL file. That's stupid! :)
  * Improved: The number of predefined paintbrushes has been doubled.
  * Added: Outline and Nibble effects for brushes.
  * Improved: The "Brush grabbing", "Zoom" and "Pipette" options are no more stopped by hiding/showing the tool-bar.
  * Improved: Now, you can change the current color while drawing.
  * Improved: The "auto-set resolution" option works better.
  * Added: The 3 color components are displayed in the toolbar when you want to choose a color.
  * Added: A small preview of the color selected by the pipette is displayed in the tool-bar.
  * Fixed: GIF saving (the bug didn't corrupt the file but resulted in a file that wasn't as well compressed as it should have been).
  * Fixed: GIF loading doesn't flash any more on some pictures that were not corrupt; and LBM neither when loading is interrupted by user.
  * Added: Menu where you can choose what you want to copy to the spare page (pixels, palette, or both...).
  * Modified: The size of the palette editor has been very slightly reduced.
  * Modified: The Stencil is now taken into account when using the "Clear" button.
  * Improved: The "magnify" mode is finally displayed with a splitted screen where you can see both zoomed and unzoomed parts of the picture.
  * Added: Now, you can load a picture from the command line (type "gfx2 /?" for the syntax).
  * Added: The preview of a PAL file is now displayed in file-selectors.
  * Modified: The tool-bar has been reduced vertically by about 1/3.
  * Fixed: Bug in the Grid menu. (The user was able to enter a null grid step. Doh!)
  * Added: "Adjust brush pick" option.
  * Fixed: DP2e (LBM-"PBM") files (including new BBM files) with odd width are now loaded correctly.
  * Improved: LBM files are now saved with their exact width and not with a multiple-of-16 witdh (viewers that can't read these files are "badly coded" because we save them correctly).
  * Improved: The selector bar is now placed on last visited directory when you change directory.
  * Added: "Mask" drawing mode.
  * Added: "Smear" drawing mode.
  * Improved: "Shade" mode options (normal, loop, saturation).
  * Added: You can define if you want Feedback (or not) while drawing in the drawing modes (effects).
  * Improved: The amount of memory used for brushes has been reduced.
  * Improved: Scrolling lists speed slightly accelerated.
  * Improved: FloodFill slightly accelerated.

## GRAFX 2.00 Beta 94.666% (03/20/1997) ##
  * Fixed: Statistics screen no longer displays that VESA 1.2 is not supported.
  * Fixed: A few bugs of no consequence.
  * Fixed: Bug in the mode-X initialization introduced in the previous version.
  * Added: It is possible to choose between Relative and Absolute coordinates in the settings menu.
  * Improved: The colors of the menu are now calculated from the current palette, so you won't have to be concerned by the colors of the menu any more.
  * Fixed: The VESA modes are no longer disabled for some video cards.
  * Imporoved: "Windows 95" keys are now usable.
  * Modified: We now use the EOS dos-extender Copyright (c) 1996 by Eclipse, so read carefully the docs if you can't use GrafX2 anymore.

## GRAFX 2.00 Beta 94.0|1|2% (02/13-23/1997) - ACE CD #4 & Volcanic3 releases ##
(These different versions were too close from each other to be separated in this file. Just check the last modifications to know which version you have)
  * Added/Improved: (approximative) HAM6 and HAM8 support in IFF(LBM) files, and improved compatibily with Amiga IFF files => should be total now.
  * Added: The absolutely useless :) CEL and KCF (KISS) file formats.
  * Added: The not much more useful SCx (ColoRIX) file format.
  * Improved: You can now use the keys to scroll the text in the Help.
  * Fixed: Small bug in the scrolling list of resolutions (1 extra line was displayed at the end of the list when current mode was 640x512).
  * Added: English user's manual translated into French (and corrected.. There can be bugs in text files :)).
  * Improved: Now, you can use the brush as an eraser by right clicking.
  * Added: X-Invert in the palette editor.
  * Fixed: Small bug in the reduce-palette function.
  * Improved: GIF saving strongly accelerated (finally!).
  * Improved: Shade mode completely modified (customized shades added).
  * Fixed: Tiny bug in the block definition of the palette editor.
  * Improved: Non-standard PCX files that don't reset the compression after each line should be supported now (at least for 256-color pictures).
  * Added: Undo in the Shade menu.
  * Added: Statistics screen.

## GRAFX 2.00 Beta 93% (12/12/1996) ##
  * Fixed: Bug that occured when approaching the borders of the screen in grid mode with the type of cursor used for brush grabbing.
  * Fixed: Small but annoying bug when saving files with a name of 9 characters.
  * Fixed: Saved PAL files no longer modify the picture's name (some mistake must have been done when we implemented the backup option).
  * Added: Now, you can stop the loading of previews by pressing a key.
  * Improved: Video cards that don't use the same VESA bank for reading and writing should now work correctly.
  * Improved: Frame displayed around the magnifier's preview.
  * Improved: Menu of resolutions completely modified, and many new modes added.
  * Modified: The default colors of the menu have been slightly lightened.
  * Improved: The whole configuration is now saved and reloaded in the settings menu.

## GRAFX 2.00 Beta 92% (11/27/1996) ##
  * Fixed/Removed: Error message occuring when accessing a drive with no disk or so finally suppressed!
  * Fixed: BMP loading was almost completely bugged and it should now be completely debugged.
  * Fixed/Modified: Set\_palette routine (the previous one was fast but did not work with some weird cards that don't support a REP OUTSB).
  * Added: Multi-Undo.
  * Added: Backup (`*`.BAK) files.

## GRAFX 2.00 Beta 91% (11/20/1996) ##
  * Fixed: Terrific bug in Help/Messages (one line was too long and crashed the program!).
  * Added: Some new parameters for the settings.
  * Added: Now, you can automatically set the best resolution for the picture loaded and/or slightly adapt the picture to keep the colors of the menu (for those who want to use GrafX2 as a viewer).
  * Fixed: Bug that occured when you wanted to restore your previous brush while being in "grab brush" mode.
  * Added: English user's manual written (will be updated later, and translated into French).
  * Fixed: No more displays pixels out of the preview window when loading corrupt pictures.
  * Fixed: Small bug in LBM loading (for non-standard widths).
  * Fixed: Minor error when saving the original screen dimensions in PKM files. (we didn't save words with Intel conventions)
  * Fixed: Exactly the same bug for LBM (but with Motorola conventions)
  * Removed: No more saving the current palette when exiting the program (that was useless and boring when pictures had a weird palette).

## GRAFX 2.00 Beta 90% (11/01/1996) - Wired'96 release ##
This version was 1st shown at the Wired'96 demo party in Belgium. We gave it to many people there, so let's start history from here. Note that there were a few different "90%" versions because we didn't want to change the number just for tiny bug-fixes.

## GRAFX 1.0? -> 1.02 (09/??/1995 -> 07/??/1996) ##
Forget it!