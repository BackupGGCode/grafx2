# Rectangles with gradation #

Selects the rectangle with gradations as the active drawing tool.

Set a corner of a rectangle. Maintain the click to move the opposite corner and release the mouse button to set it definitively.

If you don't like what you have done and want to restart, you can use the right click to cancel everything at this point. If you think it's nice, then click and hold the mouse in a point you want to have the starting color, drag to a point where you want the ending color, and release the button. You can press SHIFT to enforce your line to be vertical, horizontal, or diagonal.

# Gradation menu #

Opens a window where you can define the way gradations are processed. The different sections of this menu are:

  * Direction (arrow): Switches the direction of the gradation.
  * Dithering method: Toggles the 3 following methods:
    * No dithering
    * Basical dithering
    * Enhanced dithering
  * Mix: Mixes the gradation with a more or less random factor.
  * Palette: Select a color range to build a gradation.
  * Index scroller: Defines the current gradation among a set of 16 that will be memorised.

## Color cycling ##

These options allow you to use animation of colors: GrafX2 wil lshift palette entries at real time. Note that only the IFF file formats can record these settings, and very few image viewers will play it back.
  * Cycling: toggles the cycling of colors when you're in the editor.
  * Speed: sets the speed for the cycling of the selected range. Zero means the range isn't cycling. 1 means the range is shifted 0.2856 times per second (very slow), 64 means it's shifted 18.56 times per second (quite fast). The cycling is enabled while you hold the slider, so you can preview the current speed easily.