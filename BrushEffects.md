# Brush effects #

## Any click ##

Displays a menu where the following options are available:
  * X: Flip horizontally.
  * Y: Flip vertically.
  * Rotate by 90°: Rotates the brush by an angle of 90 degrees.
  * Rotate by 180°: Rotates the brush by an angle of 180 degrees.
  * Rotate by any angle: Triggers an interactive operation that allows you to rotate the brush. For this, start by placing the center of rotation with the left mouse button (if, at this moment, you press the right button, the operation with be cancelled). After that, you can define the angle of rotation as many times as you want by moving the mouse and left-clicking. Then validate with the right button when you are satisfied. Meanwhile, you can press on the 8 outer digits of the numeric pad for defining angles multiple of 45°:
```
                         135°    90°     45°
                            \     |     /
                             '7' '8' '9'
                       180° -'4'     '6'- 0°
                             '1' '2' '3'
                            /     |     \
                         225°    270°   315°
```
  * Stretch: Triggers an interactive operation that enables you to stretch the brush. For this, start by placing the upper-left corner of the brush with the left mouse button (if, at this moment, you press the right button, the operation will be cancelled). after that, you can place the opposite corner as many times as you need, then validate with the right mouse button when you are satisfied. If you place this point at coordinates inferior to the ones of the first point, the brush will be inverted. Meanwhile, you can press the following keys whose effects are:

  * 'D' : double the brush in X and Y
  * 'H' : reduce the brush by half in X and Y
  * 'X' : double the brush in X
  * 'Shift+X': reduce the brush by half in X
  * 'Y' : double the brush in Y
  * 'Shift+Y': reduce the brush by half in Y
  * 'N' : restore the normal size of the brush (can be useful because it's the only way for cancelling)
  * Distort: Triggers an interactive operation that allows you to distort your brush. Start by placing the brush somewhere on the screen and left-click. The brush will appear, with a little peg at each corner. Use the left mouse button to displace the corners, which will deform the brush. When you're done, click the right mouse button.

  * Outline: This option allows you to draw the outlines of the brush with the Fore-color.
  * Nibble: This option "nibbles" the outlines of the brush. It's in some way the opposite effect of the Outline option.
  * Recolorize: Remaps the brush so that it looks like it would in the spare page, using the current palette.
  * Get brush colors: Transfers the spare page's colors used by the brush to the current palette.
  * Brush handle: Allows you to choose where to place the handle of the brush.
  * Load / Save: Load or save a brush from disk.