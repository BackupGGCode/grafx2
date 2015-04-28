# Text #
The text menu allows you to enter some text and render it as a brush. The current background and foreground colors are very important, they determine the text color, the transparent color, and also the color range to use for antialiasing. GrafX2 can use 'bitmap' fonts as long as they are in the special layout supported by our version of SFont (see example fonts provided in the fonts/ directory). TrueType fonts can also be used if your version of GrafX2 was compiled with TrueType support (not the case on the gp2x, all other platforms have it by default).
  * Txt: Click and enter your text here, a line of up to 250 characters.
  * Clear txt: Empties the current text. When the text is empty, a standard string is shown instead in the preview area.
  * Antialias: Click to enable or disable Antialiasing. Only affects TrueType fonts.
  * Size: Determine the font height. Only affects TrueType fonts.
  * Font selector: Choose a font. You can use the arrow keys (up and down) to quickly browse your fonts. TrueType fonts are indicated by 'TT'.
  * Preview area: Shows what the brush will look like.