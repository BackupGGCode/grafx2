

# Installing #
## Q: (Windows Vista) The installer won't work. It fails to create a directory / write a file ##
A: Short answer: If you want to install in "Program Files", run the installer with Right-click, 'Run as administrator'.
Long answer:
I made an installer that doesn't request/require administrative rights (XP, Vista). The good part is that you can install the program even if your account is not admin on your machine. Of course, you need to choose a directory where you are allowed to write. The bad part is that the default proposed directory is in 'Program files', and normal users don't have the right to write there.

# Starting the program #
## Q: Is it possible to launch the program in fullscreen mode ? ##

A: Yes, you just have to type `grafx2 /mode <mode_name>` in a command line prompt. Type `grafx2 /?` to get the list of all the video modes.

## Q: The program doesn't start at all.. no message, nothing. ##
Check the program's directory for a file called stderr.txt. It will show the reason GrafX2 didn't start.

## Q: I changed many settings and don't like the results. ##
You can restore all settings to defaults by deleting files gfx2.cfg and gfx2.ini

# Using #

## Q: How can I set the dimensions of the picture? ##

A: We thought it was obvious that you had to click in the areas where the dimensions are written in the resolution menu (Width & Height) but many people asked this question (?!). So, to sum up, everywhere you'll see a value or text written in black in a sort of encrusted area, this means that if you click on it, you'll be able to modify its value. Moreover, if you want the picture dimensions to be the same as the ones of the screen, you just have to right-click on the resolution in the list.

## Q: Why aren't the hidden parts of the picture filled when I use the "Flood fill" tool? ##

A: For the simple and "quite" good reason that it is preferable that the user controls perfectly what he is drawing. Thus, he won't see too late that he has fucked up a part of his picture. The other tools work the same way. And for the less good reason that is was more convenient for us. ;)

## Q: The program is very slow and the mouse cursor has a lag of several seconds! ##

A: This is because you've bought a gamer mouse from Logitech or Razor, or you've foolishly "overclocked" your USB mouse port from its normal 125Hz to 500Hz or 1000Hz, even though your mouse will reports 2 or 4 times the same position...
This can also happen with a PS2 mouse, if you set the PS2 rate to 200Hz instead of classic 80Hz and 100Hz, and your PC is 10 years old and can't keep up.
GrafX2 is designed to record all mouse events in a queue, and try to take each of them into account, even if a delay is needed, in order to faithfully reproduce your mouse movements in all its details.
An unreasonable mouse rate ( > 100Hz) defeats this purpose, because it causes up to 1000 screen updates per second, and your computer just can't keep up.
Try editing the Merge\_movement setting in the gfx2.ini file. 0 means "don't merge events", a higher setting will make grafx2 skip one mouse position (or more) if there is another, more recent one in the input queue. We recommend you increase this value one by one until you don't see any lag when moving. If you increase it too much, it will be all right, except that when you use cpu-intensive functions, the cursor will seem to go in straight lines from one position to another, instead of replaying the curve where you actually moved. In practice, values of 5 and 10 should fix the problem for people who use a mouse that runs 500Hz and 1000Hz respectively.

## Q: The mouse cursor is imprecise and jumps several pixels at a time! ##

A: This is because your computer is too slow to process all mouse events one after another and merges them to go faster. Note this can happen on fast computers if you have a high precision mouse. The solution is to decrease the Merge\_movement setting in the gfx2.ini config file. 0 means "more precision", bigger values means the program will run faster, but with more cursor jumps. Values under 10 should work well enough for everyone. Do some testing to find the perfect settings.

## Q: The mouse cursor sometimes randomly becomes mad and jumps some pixels away, then comes back! ##

A: This is because Grafx2 allows you to move the cursor with a joystick instead of the mouse. Some joysticks tend to report buggy values even when you don't touch them, causing the cursor to move. Unplug your joystick and it will work better.

## Q: Help there's no menu! ##
When the menu is hidden, hit F10 to show it again (default shortcut)

## Q: How can I make the brush become monochrome, and how can I get it back to its normal state? ##

A: You can do it (assuming that you haven't modified the default keys) with the keys Shift+F4 to make the brush become monochrome, and Shift+B to get the multi-coloured brush back. With the mouse, it's Right-click on the brush selection icon, and Right-click on the Brush grab icon.

# Miscellaneous #

## Q: No sound comes out from my Ultra-maxi-sound-blaster-galaxy-64-3D-pnp, so what can I do? ##

A: Well... You must understand that this program is not a soundtracker nor a music-player :) ... So if you want some music, you'll have either to play modules with a good player, or to switch your Hi-Fi on.
Try visiting http://radio.cpcscene.com for some good music.

## Q: Where can I get the latest version of GrafX2? ##

A: The only place where you will find the latest version for sure is our web site: http://code.google.com/p/grafx2 . Nevertheless, it isn't impossible that GrafX2 may also be found on FTP or web sites dedicated to the "demo-scene" (e.g. [ftp://ftp.scene.org](ftp://ftp.scene.org)).

## Q: Why is the tool bar at the bottom of the screen instead of at the right side like in Deluxe Paint (copyright Electronic Arts)? ##

A: Well... GrafX2 IS NOT Deluxe Paint! We know that you are used to Deluxe Paint but you'll have to get used to GrafX2! ;) If you really can't stand using GrafX2 like this, then you'll have to wait for GrafX3 but we probably won't release it before year 2020! Actually, the main reason why we put the tool bar with such a basical aspect is that it was easier (therefore faster) to redraw the whole screen just by telling the routine where to stop (where starts the tool bar). Moreover, one of the best Amiga paint programs (Brilliance) has got the tool bar at the bottom of the screen too.

## Q: Will Grafx2 allow editing truecolor images ? ##
A: We won't do it. There are already many good programs that specialize in truecolor, and most of the effects in Grafx2 just don't have any equivalent in truecolor.
Note that the source code of Grafx2 is freely available under the GPL license, so anybody is free to start such project on his own. Or pick a piece of code from Grafx2 (the spline tool, an effect, anything) and re-use it in an other drawing program.