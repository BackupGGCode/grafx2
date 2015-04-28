# Drawing modes #

This button opens a menu where you can switch on or off the different drawing modes.

In this menu, the "All off" button switches all the drawing modes off. The [Del](Del.md) key is the keyboard shortcut for this button.

The "Feedback" button is only used in "Shade", "Quick-shade, "Transparency" and "Smooth" modes. When it is set, it means that the _current_ state of the picture has to be taken into account for the effect instead of the state in which the image was when you started to click for drawing. The best, as often, is that you try by yourself with and without Feedback to see the difference.

The other buttons are the following:


## Shade mode / Menu ##

It consists in increasing or decreasing the color number within a user-defined range. This shows its real dimension when used with a range of colors that shade off. Then, you can work on a part of your picture where colors belong to the same range without having to change your brush color all the time. You can choose the incrementation or decrementation of the color by pressing the left or right mouse button while drawing. If you click on a color that does not belong to the range, it will remain unchanged.

### Left click ###

Switches the Shade mode.


### Right click ###

Opens a menu where you can define one table of shades within a range of 8 memorised by the program. The different sections of this menu are:

  * Palette: You can define in it the color blocks that will be inserted into the table of shades.
  * Scroller: Used to change flick through the tables of shades.
  * table of shades definition area: The 512 squares should be widely sufficient to define the different shades since every 256 colors of the palette cannot be present more than once in each table.
  * A window (on the top-right side) permits to visualize the different shades defined in the current table.
  * Copy: Copy the contents of the table in a buffer. (Each time you open this menu, the current table is automatically transfered into this buffer).
  * Paste: Copy the contents of the buffer above in the current table.
  * Clear: Reset the "shades" table.
  * Insert: Used to insert the block selected in the palette at the cursor's position in the table of shades.
```
       IF you click with the left mouse button on this button THEN
          IF a block of more than one color is selected in the table THEN
            It is deleted and the block defined in the palette is inserted.
          ELSE
            The block defined in the palette is inserted at the postion just before the selected square.
          END IF
        ELSE
          The block defined in the palette is inserted by erasing the colors following the beginning of the block selected in the table.
        END IF
```
  * Delete: Delete the block selected in the table.
  * Blank: Follows this algorithm:
```
        IF you click with the left mouse button on this button THEN
          Replace the block selected in the table by blank squares.
        ELSE
          IF a block of more than one color is selected in the table THEN
            Insert blank squares to the left and to the right of the block.
            (this is useful for isolating a shade quickly)
          ELSE
            Insert blank squares to the left of the selected square.
          END IF
        END IF
```
  * Invert: Invert the order of the block selected in the table.
  * Swap: Allows you you move a block (this exchanges it with what is where you want to move it).
  * Undo: Cancel the last modification of the table.
  * The 2 numbers displayed on the right of these buttons are:
    * (above) - the number of the color selected in the palette if only one color is selected.
    * (below) - the number of the color contained in a square in the shades table if this square is the only one selected.
  * The "mode" button displays 3 different modes:
    * "Normal": Shades in the range and saturates to its boundaries.
    * "Loop": Shades in the range and loops if boundaries are passed.
    * "No saturation": Shades in the range and doesn't saturate if boundaries are passed. If the Step (see below) is set to 1, this option does exactly the same as the Normal mode.

  * Set/Disable: If you want to define several shades in the same table but you'd like these shades not to be effective at the same time, you can mask (disable) some parts of the table so that they will be interpreted a blank squares. To do that, select a block in the table of shades and click on "Set". The block will be underlined with a white line; this means that it is disabled.
  * Clear/Enable: This does exactly the opposite as the button above.
  * Step: Defines the step of incrementation of the shade. The bigger, the faster you run through the colors of the shade. For example: if the step is 2 and that you have defined a shade with the colors 0,1,4,5,9 and that you click on a pixel of color 1, it will take the value 5 which is 2 positions next in the table.

(We are sorry for these technical considerations quite far from a purely artistic point of view; but know that this effect is really very useful and it is preferable that you understand its whole functionment if you want to fully take advantage of it).

## Quick-shade mode / Menu ##

This drawing mode has about the same effect as Shade mode's except that it is faster to configurate but a little bit less powerful. When you draw on a color of the image which is between the fore- and the back-color in the palette, the color tends towards the fore-color (according to the step defined) if you draw with the left mouse button, or it tends towards the back-color if you are using the right mouse button.

### Left click ###

Switches the Quick-shade mode.

### Right click ###

Opens a menu with a few parameters that mean exactly the same as in the menu of Shade mode. These parameters are the step and the loop/saturation mode (normal, loop, no saturation).

## Stencil mode / Menu ##

It is used to prevent some colors from being modified if you draw on them. The main application of the stencil is when you want to change one color or more into another.

### Left click ###

Switches the Stencil mode.

### Right click ###

Opens a menu where you can define a stencil. The different sections of this menu are:
  * Clear: No color is protected.
  * Invert: Colors that were protected are unprotected and vice versa.
  * Palette: Select colors that should be protected with the left mouse button or unprotect colors with the right mouse button.

## Mask mode / Menu ##

This effect could have been called "True stencil" because it protects some parts of the picture instead of some colors. The colors you tag represent the pixels in the spare page, corresponding to the pixels in the current page, that you don't want to alter.

For example, draw a simple white figure on a black background in the spare page. Then, tag the black color in the menu of the Mask mode. When you'll draw in the current page, only the pixels corresponding to the white (non-black) ones in the spare page will be modified.

### Left click ###

Switches the Mask mode.

### Right click ###

Opens a menu where you can set the colors of the Mask. This menu works the same way as the one of the Stencil, so please refer to the Stencil paragraph to know how to use it.

## Grid mode / Menu ##

This is useful to snap the cursor to the cross-points of a grid. It's generally used to draw a grid before drawing sprites of the same size such as a font or tiles, or for drawing figures or grabbing brushes with their dimensions multiple of the step of the grid.

### Left click ###

Switches the Grid mode.

### Right click ###

Opens a menu where you can define the grid parameters. These parameters are:
  * X,Y: Steps of the grid.
  * dX,dY: Offsets of the grid.

## Sieve mode / Menu ##

This effect allows you, by defining a pattern, to draw only on particular points of the picture. If you are a Manga drawer, you might find this useful to make patterned shades or color transitions.

### Left click ###

Switches the Sieve mode.

### Right click ###

Opens a menu where you can define the Sieve parameters. This menu consists in:

  * 16x16 drawing area: You can define a pattern in it (left click => white pixel / right click => black pixel). All the white pixels indicate that, when you'll draw, pixels will be applied on the picture at the corresponding positions whereas black pixels won't modify the picture: whites pixels are the "holes of the sieve".
  * 12 default patterns: They can be copied to the drawing area.
  * "Transfer to brush": Copies the pattern to the brush (white pixels => Fore-color / black pixels => Back-color).
  * "Get from brush": Puts the brush into the drawing area (back-color => black pixels / others => white pixels).
  * Scrolling 4-arrows pad: Scrolls the pattern in the drawing area.
  * Resizing 4-arrows pad: Defines the dimensions of the pattern.
  * Default-value (black or white square): Indicates which value must be inserted when you increase the dimensions of the pattern.
  * "Clear": Sets the whole pattern with the default value (see above).
  * "Invert": It... inverts :) ... black and white pixels.

## Transparency mode (Colorize) / Menu ##

This allows to mix the color(s) of the paintbrush with the colors of the picture. It's used to make transparency effects like with watercolors.

### Left click ###

Switches the Transparency mode.

### Right click ###

Opens a menu where you can define the Transparency parameters. These parameters are:
  * Interpolation rate: Indicates the percentage of the applied color that will be considered upon the replaced color.
  * Interpolation method: Uses an interpolation algorithm to compute the color, according to the interpolation rate.
  * Additive method: Uses the lightest colors to choose the color to apply. For example: if you want to apply a color RGB:30,20,40 on a color RGB:10,50,20, the color applied will be the one, in the palette, that is the closest to the theoretic color RGB:30,50,40.
  * Subtractive method: uses the darkest colors to choose the color to apply. For example: if you want to apply a color RGB:30,20,40 on a color RGB:10,50,20, the color applied will be the one, in the palette, that is the closest to the theoretic color RGB:10,20,20.

## Smooth mode / Menu ##

It provides an easy but not as efficient anti-aliasing as any artist's touch. Anyway this effect finds a better use in making a blurry aspect.

### Left click ###

> Switches the Smooth mode.

### Right click ###

Opens a menu where you can define the Smooth matrix or choose one among the 4 ones predefined. The middle square represents the pixel on which you draw and the 8 others represent the neighbour pixels. Then, the point on which one draw will be replaced by the weighted average (according to values of each squares) of the 9 defined points.

## Smear mode ##

It smears pixels in the direction you are moving your paintbrush, just as if you wanted to spread fresh paint with your fingers. You can combine this effect with the transparency effect.

### Any click ###

Switches the Smear mode.

## Tiling mode / Menu ##

It consists in displaying parts of the brush that are adjusted on a tiling when you are drawing. It's mainly used for quickly drawing a background with a pattern, but there is a great number of other possibilities.

### Left click ###

Switches the Tiling mode.

### Right click ###

Opens a menu where you can define the Tiling parameters. These parameters are the offsets of the tiling.