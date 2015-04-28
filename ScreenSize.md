# Screen size / Safety resolution #

## Left click ##

Displays a menu where you can define the size of your picture and choose the screen resolution.

### Image size ###
Click in the boxes named "Width" and "Height" to change the size of the image you're editing, up to 9999x9999. You can also right-click a video mode to copy its dimensions to the image's.

### Pixel size ###
If you choose any Pixel size other than Normal, Grafx2 will emulate a lower resolution by scaling up everything it displays, including the menus and mouse cursor. In Double, Triple and Quadruple mode, the image will appear zoomed x2, x3 or x4, keeping the original proportions. The scaling is done in software, with no linear interpolation, so it can't cause blur.
This setting is especially useful if your hardware or drivers don't support the low resolutions you need, but it also allows you to draw in low-resolution while staying in window mode.

If you choose one of the scalers called Wide, Tall, Wide2 and Tall2, this will emulate a video mode which has rectangular pixels (longer horizontally or vertically), like some video modes of the C64, Amstrad CPC, and Commodore Amiga.

### Video mode ###
Click on a video mode to select it. Grafx2 only lists modes that are detected as available on your computer. Depending on your video card and drivers, there can be a huge difference in the number of modes it can propose. The small buttons on the left-hand side of the lines in the list of modes have been designed to allow you to disable some modes that are not supported by your card. So, the modes that you will disable won't be used  when loading pictures with "Auto-set resolution" ON.

When you click on one of these buttons, its color changes to one of the 4 following. The signification for each color of these buttons is:

  * Light gray: The video mode is OK. It can be used by the auto-set resolution option when you load picture, and you can select it in the menu of resolutions.
  * White: It works exactly the same as above. Moreover, it allows you to tag your favourite modes. Indeed, the huge number of video modes makes it more difficult to find the mode your want in the list; so you can tag your favoutite ones in white, so that it will be easier to locate them. (Note: you cannot disable the standard windowed mode)
  * Dark gray: It allows you to indicate which modes are not really perfect (flickering, not centered, etc...) but which can be used even so. The difference with the light grey button is that these modes won't be used by the auto-set resolution option.
  * Black: Use it for totally unsupported modes. Thus, these modes won't be selected the "auto-set res." and the program will not let you select them from the list of resolutions.

## Right click ##

Automaticaly switches to the windowed mode.