The brush factory is still a new feature in GrafX2, and the scripts are bundled more as examples than anything else. We are going to add more useful things in future versions. Feel free to create your own scripts and share them with us.

**WARNING: this list is out of date - need to sync it with the inline help of scripts**

# Tests and examples #
These sccripts are either unfinished, or just meant as a way to show you what's possible.
  * _tst\_AAfilter runs an antialiasing filter on the picture. However, it does not look at the actual colors but only the palette indices, so it doesn't give good results.
  *_tst\_GradientBrush replaces an existing brush with a diagonal gradient, keeping the brush size. It is a very simple script to show how a script looks like.
  * _tst\_Settings is a sample of how to draw a window from your script and handle the results._

# Brushes #
Some script render their result in the brush, so you can paste it anywhere in the image
  * bru\_db\_amigaball draws the well-known amiga boingball. It adapts the ball to the current picture palette.
  * bru\_db\_sphere renders a shaded sphere in the current pen color.
  * bru\_db\_findaa select the color in the palette that is best suitable for AA between front and back colors. Then it fills the brush with it.
  * bru\_db\_fisheye performs fisheye distorsion of the brush.
  * bru\_db\_greyscale remap your brush to a greyscale equivalent. There are two versions of it, Desat and Average, using different math.
  * bru\_db\_halfsmooth reduce the brush size by half, using some smoothing techniques to make it look better than the default way provided in GrafX2.
  * bru\_db\_mandlebrot draws a mandelbrot fractal in the brush. The size can be set as well as other options.
  * bru\_db\_waves distorts the brush in waves.

# Palette #
Palette operations can be automated. This include generating palettes, or modifying the current one. Custom remapping involving the spare page palette may also be done.
  * pal\_db\_desaturate desaturates the palette by a given amount. The result is a washed out picture.
  * pal\_db\_expandcolors Continously fill the greatest void in the area of the color-cube enclosed by (or along ramps of) initial colors. This algorithm will create lines of allowed colors (all ranges) in 3d colorspace and the pick new colors from the most void areas (on any line). Almost like a Median-cut in reverse.
  * pal\_db\_FillColorCube creates a color cube palette in a given range of colors. This can serve as a base for building your own palette.
  * pal\_db\_invertrgb Arbitrary name for the function ch1 = (ch2 + ch3) / 2. It produces something close to complimentary colors. Ex. Yellow --> Bright Blue, Blue --> Dark Yellow. Mostly just a nice effect and it shows how you can easily manipulate the palette.
  * pal\_db\_set**generate a palette.
  * pal\_db\_shifthue shifts the hue (color) of the palette.This does the same as the H-slider in the palette screen, but you can use this one as a function in other scripts.**

# Picture #
More interesting are the scripts that run on the whole picture. These don't touch the palette. They are either distorting the picture in some way, or rendering something from the palette.

  * Pic\_db\_pic2isometric convert part of the picture to an isometric version.
  * pic\_db\_rainbow\_dark2bright draws a color rainbow. This helps spotting missing colors (rainbow holes) in a work in progress palette.
  * pic\_db\_sierpinskicarpet draws a Sierpinski carpet.
  * pic\_db\_sierpinskitriangle draws a Sierpinski triangle
  * pic\_ni\_cellcolourreducer allows to reduce the colorcount in 8x8 or other size blocks to 2. This is often a constraints on old 8bit microcomputers.
  * pic\_ni\_drawgridisometric fills the picture with an isometric grid.
  * pic\_ni\_drawgridorthogonal\_ind draw an orthogonal grid
  * pic\_ni\_drawgridorthogonal\_rgb ??? should be merged with the two above.
  * pic\_ni\_flippicture ??? does the same as the flip effect in transform menu.
  * pic\_ni\_glassgridfilter does a "glass grid" effect on our picture.
  * pic\_ni\_palettetopicture is the easiest way to convert a palette to a picture for easier sharing.
  * pic\_ni\_xbitcolourspacefrompalette does quite the same as rainbow, but in a different way.

# Scene #
These change both the palette and the picture to render a full scene. They may still use the original picture in some way, such as when doing palette remapping.

  * scn\_db\_remapimage2rgb remaps the picture to a pure RGB palette (4 colors) with custom dithering in diagonals
  * scn\_db\_remapimage2RGB\_linedither ??? should be merged with the above. Same, but different dithering method.
  * scn\_db\_remapimage3bitpal ??? merge with others ?
## Animation ##
It is possible to do some animation while a script is running.
  * ani\_db\_Ellipse draws a moving ellipse. It's the simplest script with animation features.
  * ani\_db\_spritesheet animates a sprite from a sheet in the spare page. It's quite limited right now, but allows you to draw animated stuff and easily look at the animated result.