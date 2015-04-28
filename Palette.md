# Palette menu #

![http://grafx2.googlecode.com/svn/wiki/pictures/palette.png](http://grafx2.googlecode.com/svn/wiki/pictures/palette.png)

## Left click ##

Displays a menu where the following options are available:
  * Palette: Allows you to choose a color-block to edit. If you click with the right mouse button, you'll choose a new Back-color.
  * Gauges: Allow you to modify the current selection.
  * "+" and "-": Allow you to lighten or darken the current selection.
  * Default: Restores the predifined GrafX2 palette.
  * Gray: Transforms the current selection into its gray-scaled equivalent.
  * Negative: Transforms the current selection into its reverse video equivalent.
  * Invert: Swaps the colors of the current selection so that the first colors become the last one.
  * X-Invert: Works as above but modifies the picture so that it looks the same.
  * Swap: Swaps the current selection with another color-block. Click on the beginning of the new color-block.
  * X-Swap: Works as above but modifies the picture so that it looks the same. This may be useful if you want to sort your palette.
  * Copy: Copies the current selection to another color-block. Click on the beginning of the new color-block.
  * Spread: Computes a gradation between two colors. If your selection is only made up of one color, select the second color in the palette. Otherwise, the two colors used will be its extremities.
  * Sort: sorts the palette by color ranges. If you click with the left mouse button, it will sort by H S L; and if you click with the right mouse button, it will sort by L only. Note that you can choose a range of colors before sorting, and instead of the whole palette it will sort this range.
  * Used: Indicates the number of colors used in the picture.
  * Zap unused: Erases the unused colors with copies of the current selection. (The keyboard shortcut for this button is `<`Del`>`).
  * HSL: Switches between RGB and HSL color spaces. In HSL mode, the three sliders allow you to set the Hue (tint), Saturation (from grayscale to pure color) and lightness (from black to white).
  * Reduce: Allows you to reduce the palette to the number of colors you want (and modifies the picture).
  * Undo: Allows you to recover the last modifications made on the palette. If the last operation modified the picture, it won't recover them: you'll have to click on Cancel to do so.

If you press `<`Backspace`>`, the program will replace, as well as possible, some unused colors by the four default colors of the menu. The image won't look altered because the modified colors (in the case they were used on a few points) will be replaced by the closest colors in the rest of the palette. This option is really useful when you modify the palette so that there are no colors that fit for the menu (eg: "Zap unused" while very little colors are used in the picture; or "Reduce" with a very small number of colors).

If you press the key below `<`Escape`>` or `<`,`>` (QWERTY), the menu will disappear and you will be able to pick up a color from the picture easily. Press `<`Escape`>` to cancel.

If only one color is selected (not a block), the `<`[`>` and `<`]`>` keys can be used to select the previous or next Forecolor (Backcolor if you press `<`Shift`>` at the same time).

Warning! If you press Undo after an action that modifies the picture (X-Swap, X-Invert and Reduce colors), the picture won't be remapped as it was just before this action. Only Cancel will.

## Right click ##

Opens a menu from where you have the following options:

  * Colors for best match: A menu in which you can select the colors that have to be used for smoothing, the transparency mode, and for remapping.

  * User's color series: A menu in which you can define color series for next/previous user color shortcuts. It's the same settings than the shade mode. After you have some color ranges defined in this screen, you can use those shortcuts to move to the next or previous color according to your ranges.

  * Palette layout: lets you customize the palette that appears on the right of the menu. You can choose the number of lines and columns. If you want the colors to run top to bottom, check the "Vertical" button, otherwise the colors run left to right.

  * RGB scale: lets you select the scale of the R G B sliders in the palette screen. You should normally leave it at 256 to get the full 0-255 range, but if you want to constrain the palette to the capabilities of some specific computers and consoles, you can choose eg:
    * 64 for VGA
    * 16 for Amiga / Atari STe / Amstrad Plus
    * 8 for Atari STf
    * 4 for MSX2
    * 3 for Amstrad CPC
    * 2 for ZX Spectrum

## Resources ##

Some users sent us their palettes to share with you. Check out this page to download them : http://code.google.com/p/grafx2/source/browse/#svn/branches/pic-samples