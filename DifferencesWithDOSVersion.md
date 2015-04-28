If you have been using the DOS version of Grafx2 (or still using it through DOSbox), the following information will tell you how Grafx2 adapts to the new platforms.
Even if you've been using the Win32 port by Eclipse-game, some of this information may interest you.

# Operating system and Endianness #
The program works on Windows or Linux (and others), and on little-endian or big-endian CPUs.
It also compiles and runs fine on 64bit systems.

The developers are testing on:
  * PulkoMandy
    * A gp2x f100 mk2 (ARM CPU, Custom linux)
    * A Dell inspiron laptop with 64bit cpu, Linux.
  * Yves
    * A desktop PC (little-endian) Windows 98.
    * An IBM laptop (little-endian) Debian linux (Gnome) and Windows XP.
  * Hitchhikr
    * An Intel macintosh.
  * Peter Gorgon
    * An AmigaOne XE-G4 PowerPC (big-endian), AmigaOS 4.

GrafX2 doesn't run on iPod, Nintendo DS, nor your toaster yet. Sorry :). Feel free to offer your help for a port.

# File system #
Long file names are accepted. The Save/Load screens have been adapted to show up to 28 characters for the current file name, but the area can scroll right and left as needed to allow editing of longer filenames.
Character encoding is the one known as Latin-1, or Windows-1252, or Western European.
The "drives" icons have been replaced by a "Select drive" button that allows you to choose between the drives (windows), or "/", "$HOME", and mount points (linux) and volume names (Amiga).
On all platforms, the files are sorted in a case-sensitive way, but the "quicksearch" feature is case-insensitive.
The list of drives is queried whenever you click the button, so you can use drives that are added dynamically, for example when you plug a USB memory stick.
There are 4 dropdown boxes allowing you to save your favourites folders and reach them quickly.

# Library #
The program uses SDL instead of direct hardware calls and VGA / VESA. This affects the following:
## Mouse ##
The mouse cursor should use exactly the settings of your OS. Grafx2 no longer needs its own mouse settings.

The program allows you to bind shortcuts to your third mouse button and mouse wheel, in combination with shift / ctrl / alt if you want. 4th mouse button (etc) still not supported.
## Keyboard ##
You can type filenames normally, the right characters will appear (within the limits of Latin-1 character set). Pressing control C in text input boxes no longer crashes the program.

The keys for keyboard shortcuts, unfortunately, may not behave as expected on all platforms. On Windows, SDL reports keys as if they were on a US QWERTY 105-key keyboard. This means the key names as shown on the configuration utility will not match the key labels. On the other hand, a benefit is that the default keyboard settings will suit well for all windows users who have a 102 / 105-key keyboard, whatever its localization.

In any case, the key combination you type yourself when setting a shortcut will work identically in the program. Only the key name display may be wrong.
Now any key can be bound, as long as the OS / Window manager doesn't trap it.
Ex: Debian's Gnome catches PrintScreen and displays a screen capture window, GrafX2 doesn't get this key.
## Video modes ##
The program's default mode (and 'safety resolution', the one you can call with Shift+Enter) is now a scalable window, since this is guaranteed to work on all platforms and screens. You can resize or maximize the window using your normal window manager, dragging the window edge etc.
The other modes are fullscreen, using whatever technology provides fullscreen modes on the OS (DirectX on Windows, X11? on linux)
The program has a preset list of (low-resolution) modes, and checks with SDL if each of them is supported. It also queries SDL for more resolutions, and all modes auto-detected by SDL are added to the list. The resolution screen only shows video modes that SDL claims it can display. If your graphics cards reports a mode that outmatches your monitor's capacities, you can tag it "Unsupported" by clicking the left-column button until it displays a black block. This way, GrafX2 will not use this mode on your system.

About color depth: Grafx2 is still a 256-color program, and will use 256-color mode if they are available. If your hardware or driver only support truecolor/hicolor modes, it will use them instead, SDL does an excellent job of converting on-the-fly 8b->24b.

On modern hardware, it's common to have very few resolutions proposed. On windows you can try to use the program Powerstrip to unlock more resolutions, at your own risks. (Use "Low resolution mode calculator" lrmc to compute resolutions parameters, to feed Powerstrip). On Linux you can try with xvidtune. In any case, if you are using a LCD monitor, you're limited to resolutions which are a multiple of your monitor's native one.

However, Grafx2 now proposes a software pixel scaler, to emulate lower resolutions. This works on all platforms and all modes, as long the resulting surface leaves enough room for the menus. For example in 1024x768 fullscreen, you can use "double pixel" mode to obtain 512x384. This works even in windowed mode, so you can use it to draw low-resolution graphics while staying in your 1600x1200 desktop.

The scaler can even make rectangular pixels (1x2, 2x1), allowing you to emulate some C64 / Amstrad / Amiga modes.

# Color precision #
The DOS version was limited to 18bit palette entries , like the VGA hardware. (R G B on a 0-63 scale) The new version has 24bit precision, so you can set Red, Green, and Blue on a 0-255 scale.

Grafx2 would originally strip the low bits of colors from some file formats (ex:GIF) when saving, now it no longer does : For example a "magic pink", often used to mark transparency in game graphics, now stays (255,0,255), instead of being approximated to (252,0,252).

# Power saving #
The original GrafX2 is a single-tasking DOS program, it uses all available CPU cycles. This version reduces the cpu usage to what's actually needed, to make it usable on laptops.

# Ascending compatibility #
Grafx2 can load configuration files (grafx2.ini and grafx2.cfg) from the DOS version. It will recover as much of your keyboard shortcuts, options, stencil tables, shades, etc. as possible.

# Image file formats #
Grafx2 can still save & load the file formats originally implemented. PNG and Neochrome are now available. The BMP loader has been debugged and improved to load more BMP variants. The PKM file format still uses 18bit colors, so when saving images in PKM format your palette loses some precision, you should use some other format like GIF or PNG, for example.

# New features #
All the missing features from the dos version are available. Gradiation rectangles, text (both ttf and bitmap), brush distortion and some picture effects.
The program is also fully skinnable. The GUI has been improved, to make it behave more like modern things (click buttons on mouse release, don't leave a slider while the mouse is clicked for example). Simple support for dropdown menus was added.

# Online help #
If you forgot some shortcut or can't get a tool to work like you want, just remember that you can press the F1 key at any time. That will open a window with some text about the active tool, opened window, or the button you are hovering with the cursor in the menu.
The window will remind you how to use the tools, shows you the current keyboard shortcut(s), and allows you to change them.

# Bugs #
Unfortunately, we've introduced some bugs in the program while modifying it to run in the new platforms and remove the hardware-dependant parts. There are also some cases where a bug was present in the original code, but undetectable and harmless in DOS due to the lack of memory protection, and yet it will crash the program on a recent OS.
If you ever find one of them, please report it in the issue tracker...