# Hand-drawing #

## Left click ##

Selects the current hand-drawing mode as the active drawing tool. There are 4 hand-drawing modes:

  * Continuous hand-drawing: as you move the mouse, the paintbrush is regularily pasted on the picture. This drawing tool allows to change the fore and back colors when being in use.
  * Discontinuous hand-drawing: as you move the mouse, the paintbrush is pasted on the picture every time a delay is passed (the delay is fixed to 20ms). This drawing tool allows to change the fore and back colors when being in use.
  * Dot by dot hand-drawing: the paintbrush is only pasted at the position where you first clicked.
  * Contour fill: Draws pixels like continuous mode, but when you release the button Grafx2 draws a line back to your starting position, and fills the area. This tool doesn't use the current brush, but single pixels.

## Right click ##

Toggles the different hand-drawing modes and activates, at the same time, the hand-drawing tool.