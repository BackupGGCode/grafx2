# Drawing tips #

This section deals with tips that can help you to draw some cool effects, or just to draw faster. Note that, in most cases, these tips only make a big part of the work and that you'll have to touch up in zoom mode if you want to draw a picture worthy of the name! ;) Moreover, if you've found out nice tips by yourself, and if you want to share them with the others, don't hesitate to tell us.

## Anti-aliasing ##

This is not an effect proposed by GrafX2 but a drawing method. It consists in placing medium colored pixels in the angles formed by contrasted pixels for artistically smoothing their aspect. From our point of view, this is essential for drawing really nice pictures. An easy but tiresome way (the best way!) is to start by adding 1 middle color, then antialias the new colors "recursively" while you have intermediate colors in your palette.

```

                           ############
                                       ############

                           ########±±±±±±±±
                                   ±±±±±±±±########

                           ####MMMMM±±±±xxxx
                                  xxxx±±±±MMMMM####
```


## Smear mode combined with concentric lines ##

By combining this effect and this drawing tool, you can spread an area from a central point. If you aren't in high resolution, it can be useful to switch on the transparency mode too (see next section).

A possible application is to draw fluffy hair. For that, you can choose one of the pre-defined paintbrushes loking like random points. According to the hair density you wish to obtain, you can choose a paintbrush with more or less points. Then, place the center of the concentric lines in the middle of the plush, and rotate the mouse around it keeping the mouse button pressed. With the same method, by turning around more, you can manage to give an explosion effect to an object.

You can also create easily and quickly sun rays with this method. For that, after having drawn the primary shape of the sun in the sky, choose a paintbrush according to the size of the rays you want (but a small one will often be prefered), and place the center of the lines in the center of the sun. Then trace the ray at the length you want. If you didn't take a big paintbrush, you'll be able first to draw an aura around the sun by rotating quickly, and then to add more important rays with precision.

## Smear mode combined with Transparency mode ##

These two drawing modes, once combined, permit to spread parts of the picture as fresh paint. It is recommanded to use the transparency method which consists in interpolating with an opacity of about 60% and the effects "Feedback" on.

As in the przvious section, it can be useful for drawing hair and especially eyelashes if you have got a good palette (i.e. a palette that contains color gradations between every colors you'll draw on during the operation. For drawing eyelashes for example, after having drawn the eye and the eyelid, trace a quite thick black line representing the base of the eye-lashes (this is that black line you'll spread out on the eyelid). Then, in smear+transparency mode, draw with the freehand continuous tool (with a small paintbrush: 1, 2 or 3 pixels wide according to what you draw: a face or a close-up on an eye) starting from the base of the eyelashes in giving their shape. You'll see your black bar looking more and more like eye-lashes.

One can also use these effects for mixing colors on the screen like paint. For example, if one want to draw a background made of abstract shapes composed of color mixings, one can proceed like what follows:
  * Define a palette containing a gradation between the different colors you wish to use .
  * Draw very vaguely the different colored areas with a big paintbrush (in normal mode).
  * With a smaller paintbrush, and with the spray, apply these same colors but lighter or darker on the previously defined areas.
  * Always with the same paintbrush in spray, but this time in smear mode (not necessarily with transparency... but why not?), mix all these colors on the screen to obtain a "multicolored pulp" vaguely conserving the different color areas.
  * At last, in Smear+Transparency mode, with a medium rounded paintbrush, hand-draw by whirling or making waves, etc... conserving the same movement to avoid breaks. This aims at eliminating the pixellisation made by the spray and giving the final mixed paint aspect.
  * Now, if it's ugly, it's either because my explanations are incomprehensible, or because you have no talent! :p

## Spray combined with shade mode ##

If you often use Shade mode, and you are tired of clicking plenty of times on a pixel for reaching the color you want, you can define a spray with "Size"=1, "Mono-flow"=1, and "Delay"=2 (or more, according to your reflexes). Then you'll just have to click a few hundredth of second for modifying a color.

With a wider diameter, it permits to add granularity to a texture, because placing lighter or darker pixels creates some ruggedness. Different textures appropriated to this effect are: sand, rock, etc... Of course, you'll need a color gradation corresponding to color of the texture.

You can also draw more elaborated textures using a paintbrush of the shape of a small curve or line as these figures "try" to show. ;) Thus, you can create textures of straw, hair, rock, marble (although hand-drawing would be more recommanded than spray for this last one).

```
\      _
 \      \
  \     |
```

## Shade mode used for replacing a color gradation by another one ##

If you drew something with colors belonging to a gradation and you'd like to  replace all these colors by the ones of another gradation (with the same number of colors), proceed as follows:
  * Define these 2 gradations in the same shade table in the shade menu without separating them by a blank square.
  * Set the "no saturation" shade mode.
  * Define the step of the shade with the size of the two gradations (e.g.: enter 16 if each gradation contains 16 colors).
  * Now, you just have to draw on the area you want the colors to change (with the left mouse button if you placed the gradation to replace first in the shade table, or inversely).

## Spheres combined with additive transparency mode ##

Starting from a dark background (if possible all of the same color), trace overlapping spheres with their lighting point at their center. You'll quickly obtain a "blob" effect.


## How to draw drops ##

Here is a fast and efficient method to draw drops. Just draw very bright pixels on the side of the drop where the main light is, and less bright ones on the opposite side. Then draw shadows according to the position of the light.

Here are examples with a light coming from the top-left corner.
You may think that the smallest  drop doesn't really look like a drop, but draw it in graph mode and you'll see it DOES look like a drop.

```
±±±±±±±±±±±±  ±±±±±±±±
±±±±±±±±±±±±  ±±±±±±±±
±±±±²±°±±±±±  ±±Û°±±±±
±±±²Û°°±±±±±  ±±±°²°±±
±±±Û²°±²°±±±  ±±±±°±±±
±±±²±°²²°±±±  ±±±±±±±±
±±±±±²Û±°±±±  ±±±±±±±±
±±±±±°°°±±±±
±±±±±±±±±±±±
±±±±±±±±±±±±
```

If you don't trust me, then know that it's by looking at Lazur's graphs that I found this method. And in a general way, it's always good to study the work of the best artists to learn new techniques.

## Load a picture adapting it to the current palette ##
**Open an image with the right palette** Switch to the spare page (tab)
**Load the image you want to adapt** Switch back to first image (tab)
**Open the 'copy to spare' menu (shift-tab)** Choose 'palette and remap'

## Replacing colors ##
If you want to change the color mapping in a small part of your picture, you probably noticed that you can't use the 'color replace' tool as it will replace things in the whole picture.
Here are good ways to do it :
  * Using the stencil, you can tag all the colors except the one you want to replace. Then you can use any drawing tool to alter the color in one area of the picture without touching other colors
  * For remapping a full tile in a sprite sheet, it's usually simpler to copy it to the spare page and remap it there with the color replace tool, before copying it back.
  * To recolor a full sprite (for example if you want red, green and blue versions of the same sprite), you can use the quick-shade feature. If you have shades all of the same size and sorted in the palette, setting Quick Shade step to the shade size will make pixels jump from one shade to the following one when you click on them. Using it with 'feedback' disabled allows to easily recolor a sprite in one operation.