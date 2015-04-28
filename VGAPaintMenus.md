I've wrote down the menu scheme of VGA paint so we can easily look what is in it.
I've checked (X) features we don't have.

Project
  * New
  * Load
  * Save
  * Save as
  * Bitmap size
  * Transform
    * Flip X
    * Flip Y
    * Rotate
  * Overview (hide all menus)
  * Info
  * Print
  * About (nice rotating animated logo in the about window ! we need that :D) (X)
  * Quit
Brush
  * Matte (our monochrome mode)
  * Color
  * Opaque (X) (256 visible colors in brush)
  * Palette
    * Change transp (X) (brush transparency is independant from bg/fg color)
    * Remap to palette
  * Orient
    * Flip X
    * Flip Y
    * Rotate 90°
    * Rotate free
  * Handle
    * Cycle
    * Center
    * Place (X) (not implemented in vgapaint either :/)
  * Resize
    * Halve
    * Double
    * Double X
    * Double Y
    * Free scale
Anim (X) (yes we miss the whole menu :))
  * Load
    * VAN
    * Multiple PCX
    * AVI
  * Save
    * VAN
    * VAN with audio
    * PCX
    * ANI (windows animated cursor)
    * FLC
  * Next frame
  * Prev frame
  * Goto frame
  * Forward play
  * Play once
  * Ping-pong
  * Add frame before
  * Add frame after
  * Delete frame
  * Set framerate
  * Frame palette
    * Attach from next
    * Attach from prev
    * Attach new
    * Detach
    * Detach all
    * Separate
  * Anim palette
  * Process
    * Feather palettes
    * Anim palettes
Special
  * Palette
  * Arrange (palette management)
    * HSV Spread (provide saturated gradations even if you go from yellow to blue) (X)
  * Ranges (shade tables used for gradation, shade, and color cycling anim)
  * Dither (X) (but do we need that? it upscales the picture and reduce color count)
    * 640x480x16
    * 1x1x1 RGB
    * 640x480x2
  * Process
    * 3x3 average rgb (each pixel is replaced by the average of the 8 pixels around. new palette is created for this) (X)
    * 5x5 average rgb (X)
    * 3x3 median rgb (X)
    * invert
    * color most > least (sort color by number of pixes using them) (X)
    * color least > most (X)
    * merge same colors
    * pcx-optimize (sort palette to make pcx compression better) (X)
    * delta horizontally (each pixel is replaced with his difference from the previous one. allow better compression.(X)
    * delta vertically (X)
    * un-delta horizontal (X)
    * un-delta vertical (X)
  * re-pics (draw something to the current page) (useful for quickly testing a palette ?) (X)
    * Color chart
    * RGB bars
    * Rainbows (HSV bars)
    * Plasma
    * Gamma test
    * Maze
    * Default palette (convert current image to default ms-dos vga palette)
  * Spare
    * New (X)
    * Swap
    * Copy from spare
    * Spare list (X)
    * Get palette
    * Fit to palette
    * Merge
    * Delete
    * Underlay (color index 0 in current picture is replaced by corresponding pixel in spare) (X)
    * Overlay (X)
  * Tone (X) (no space left in our palette screen...)
    * Brightness / Contrast / Gamma
    * Color balance
    * Color control
  * Convert
    * Greyscale
    * Black&White
    * Grey 256-level
    * Grey 64-level
    * Grey 16-lev
    * Grey 8-lev
  * Fill mode
    * Normal
    * Tile (from brush) (X) (we have simple 2 color patterns, but this can be used with tiles)
    * Stretch (from brush) (X)
    * Stretch&blend (antialias stretch) (X)
    * Horizontal (does nothing)
    * Vertical (does nothing)
    * Horiz gradient (X)
    * Vert gradient (X)
    * Color range (select gradient to use for horiz and vert grad mode)
  * Draw mode
    * Normal
    * Range FWD
    * Range back
    * Color range (same as our shade window)
  * Line mode
    * Normal
    * AA (always with the same color) (X)
    * AA+blend (get AA color from existing pixels) (X)
  * Blit mode
    * Normal
    * Transparent
    * Add
  * Tile mode (in zoom mode, instead of using colors you draw with 16x16 tiles from the spare page) (X)
Pref
  * Video driver
  * Capture mode (for capturing screens from other dos programs) (