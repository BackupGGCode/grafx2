# GrafX2 - Input interface #

## `Get_input()` (in DIVERS.ASM) ##
### Keys ###
Updates the global variable "Touche" (="key"), a 16-bit word containing in its lower part the scan-code (value linked to the location of the key) of the key pressed, and in its higher part a code defined by the control keys pressed during the call.
  * (Touche & 0x0100) => Shift
  * (Touche & 0x0200) => Control
  * (Touche & 0x0400) => Alt
Put in the global variable "Touche\_ASCII" the ASCII code (value linked to the character represented by the key) of the key pressed.
If the global variable "Autoriser\_changement\_de\_couleur\_pendant\_operation" (="allow color change during operation") is set to 0, and if there's at least one value in the operation stack, the function filters the keys. This means that one can't interrupt an operation in progress, except for changing the color of the paintbrush if the operation permits it (useful for changing the color of the paintbrush with the keyboard while drawing).
### Mouse ###
Updates the position (Mouse\_X,Mouse\_Y) of the mouse according to its position in a virtual screen. This screen is voluntarily bigger than the actual resolution of the video mode because several mouse drivers don't provide the position of the mouse precisely (pixel by pixel)...
Updates the state of the buttons of the mouse (Mouse\_K). This variable is set to 0 if no button is pressed, 1 if the left button is pressed, and 2 if the right button is pressed.

If more than one button are pressed, Get\_input() considers that no button is pressed (Mouse\_K = 0).

The function corrects the position of the mouse to prevent it from leaving the current drawing area if the operation stack is not empty (the mouse does not leave the drawing area while the drawing operation is not finished), and it also simulates the movement and clicks of the mouse if the current key combination corresponds to such commands. In this latter case, the keys are filtered to prevent the calling function from working for nothing.

If the state of the mouse changes or the global variable "`Forcer_affichage_curseur`" (="force cursor display") is set to 1, the mouse cursor is displayed. This fonction always sets Forcer\_affichage\_curseur to 0 at the end of the call.
The function calls `Calculer_coordonnees_pinceau()` (="compute paintbrush coordinates") which is in charge of the computation of the coordinates of the paintbrush (Pinceau\_X,Pinceau\_Y) ("Pinceau"="Paintbrush") according to the position of the mouse on the screen, the position of the drawing area in the image, the zoom factor and the grid effect.

Important: In most cases, you won't have to call this function because the engine (main loop, window manager, file selector, ...) has already done what is necessary. You can therefore consider the concerned variables as already updated. If you called `Get_input()` yourself at an inappropriate moment, some commands of the user, taken into account by the engine, might be ignored.

## `Attendre_fin_de_click()` ("Wait end of click") (in DIVERS.C) ##

If you need to ensure that no mouse button is pressed by the user at a certain moment, this function waits until the user releases the button. Then, Mouse\_K equals 0, but if the mouse has moved during the waiting, its position (Mouse\_X,Mouse\_Y) is not yet up to date. However, this shouldn't be bothering (at worst, a simple call to Get\_input() will update these values).

## `Readline()` in READLINE.C ##

This function is used inside windows to let the user input something with the keyboard. For example, it's used to get the filename when saving, to get the size of the picture in the resolution window.