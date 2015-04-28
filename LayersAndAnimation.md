# Introduction #

Two of the big features we plan to add in GrafX2, layers and animation, need a
rewrite of the management of pages in the program. This page gather the ideas
and possible designs and is open for discussion.

# User interface overview #
## Animation ##
The idea is to provide a full animation package allowing to create full
video sequences. This would be based on effects applied to layers : rotation,
distorsion, movement and zoom. We also provide regular animation with simple
frame switching and different drawings on each frame, and palette cycling.
It's not so easy to combine all this in one coherent interface.

The timeline is the main thing we create when we open a file. It is possible to
render a specific frame to the screen. Rendering all the frame according to
their timestamp will play the animation. Rendering only one frame allows to
preview it. It is possible to switch between frame preview and layer edition.
It is not possible to paint on a frame, because the layers can be rotated, zoomed,
distorted. You have to select a layer and show it in 1:1 pixel mode to edit it.
In this mode the other layers are no longer linked to the selected one, so you
edit only one layer, on a black background. We could use the splitscreen system of
the zoomed view to display both the frame rendering (as the normal view) and the
edited layer (as the zoomed view).

An animation is a set of frames arranged in a timeline. Each fram can have a
different palette, so it is possible to use them to do simple palette cycling
animations. They also hold a list of layers. Each layer is composed of two
parts: picture data and distorsion information. Picture data is the real set of
pixels. The same picture data can be used in multiple layers, either in multiple
frames (this is what happen when you do palette cycling: the same pixels are
dispayed over and over, with a different palette). The distorsion is the
position, rotation, stretch and linear distorsion of the layer. It can be
handled pretty much like the current "brush effects" screen. So you can have a
part of your picture scrolling over the screen while rotating, if you want.

Different palette for each animation step: I don't like it very much, as it's
quite painful to keep the palette consistent over the different frames, and I
really doubt it's well-supported in GIF format (the specs says yes, but I've
seen how web browser and Windows image editors don't support the specs for
animation). Palette animation is something you generally do without changing
pixel data... I suggest we implement it like Deluxe Paint, completely
independant from image animation. This will not allow to do things like
fade-in/fade-out in a moving animation. I think we can have a "palette cycling"
interface in the palette menu, and a more powerful palette management in animation
mode, both using the same backend.

I saw some quite advanced features in picfmts.doc (don't remember which format),
in this one it was possible to have each cycling step stay on screen for a
different amount of time, and the cycling going once, in a loop or in "pingpong"
mode. So I tought it made sense to use the same timeline system as the other
animation features. This is practical for us on the code size, not meaning we
enforce people to use both features in their works. If the cycling is independat
from the animation, it means it is not possible to change the palette in an
animation in any easy way, and it also means we go for a very simple cycling
scheme with colors looping in an endless loop and staying each for the same time
on screen. I find that a bit sad. Remeber we are trying to be the ultimate 256
color painting program ;)

There is a thing that i'm not sure: should the spare page be also an animated
timeline ? or should just it be a still frame with fixed layers ? or just a
single page ?

## Layers ##
There are two ways to use layers :
  * In a still picture, the photoshop way. (this is what a layer usually is)
  * In an animation, which is what I was thinking of when writing this page. In this case a layer is used as a sprite and can be stretched, rotated and distorted. But to draw on it, it is important to have an undistorted view. When working on an animation, we want to display only the active layer. When working on a still picture, we want to display all of them. Maybe the two modes are too different and incompatible, or maybe we can find a way to make them work together.

Proposition of UI for the 'layer' buttons, inspired by Artgem and completed with
experiments with a tile editor which supported layers :
  * Each "layer" button shows one of 3 possible states : Hidden, Visible, Visible+Current (where you draw)
  * Only one layer is Current at a given time.
  * Clicking a non-current layer with RMB: toggles it visible on/off
  * Clicking a non-current layer with LMB: it becomes (visible and) Current.
  * Clicking the current layer with LMB:
    * Not effect. Maybe we can use it to initiate drag-n-drop operation: dropping on another layer button will cause a translation of the current layer to target position.
  * Clicking the current layer with RMB:
    * If it's the only visible layer, all layers become visible,
    * Else, it makes all other layers invisible.
![http://i26.tinypic.com/25ivjbo.gif](http://i26.tinypic.com/25ivjbo.gif)

The number of layers is limited anyway, because we can't put an infinite number
of keyboard shortcuts... "Switch to layer 1", "Toggle layer 4", etc. One very
handy keyboard shortcut can be to "Toggle current layer", because it will switch
from "all layers" to "only the current layer", just like when you right-click
the current layer.

Further experiments with UI:

![http://i32.tinypic.com/rhl7vl.jpg](http://i32.tinypic.com/rhl7vl.jpg)

The vertical layouts are the most natural, since the "bottom" layer is the
background, and the one over it are piled on top of each other. But the size is
VERY limited as it makes tiny buttons, 8 layers is really a maximum. The buttons
are still bigger than those in ArtGem though, even when the menus are not zoomed.
Some of the vertical scemes remove the separation between the 4 parts of the menu
(tools, effects, settings, palette), which does not seem a good idea. The
separation bars could be made thinner if we need some space, but I prefer we keep
them. I think the layers would be part of the settings+management part, along with
brushes.

Horizontal layouts allow more layers, but make the menu bigger (when layer row
is displayed). The horizontal layerbar provide a button to show or hide it. This
is a good idea, however the button to do the same with the menu is in the status
bar. It'd feel strange if hiding the statusbar also hide the menu but not the
layerbar. I like this system as we also will need an animation bar and maybe
some others. The layer buttons are not aligned with the buttons in the menu, but
this can't be solved. Not really a big problem. The "Layer" button in the bar
should use the same font as the KILL and PAL buttons.

Ilkke suggested to replace the Hide button with one to switch between multiple
toolbars/modes. The default position would be the current one, left click would
switch from/to animation mode (timeline, keyframes management, playing speed,
looping mode (no loop/loop/pingpong), play, stop buttons, etc.). RMB would
switch the menubar off and stay in the current mode (useful in animation mode to
watch your work in fullscreen). Maybe the layer part could go either on a third
bar or with the animation. However this is unpractical when drawing a still
picture if you want to switch quickly between the layers... Combining this with
the "stackable toolbars" idea seems nice.

Possible alternative: button opens a popup menu to choose which toolbar(s) are visible:

![http://i27.tinypic.com/6ptc7o.gif](http://i27.tinypic.com/6ptc7o.gif)

Another solution is to keep the menu as it is and use the space where we have the
palette as an area where you can display palette or layers or animation. The
settings/load/save part of the menu could be moved there as well (you don't use
it often).

I'm not sure it's easy to remember which number is attached to which layer.
Maybe a preview system (like the one in the load/save) screen could be useful
for that. This could also allow easier palette sorting, maybe (with a list of
layers and some move up/down/top/bottom buttons). Button dragging mean we have
to write special code for draggable buttons. But could be nice for quickly
moving things around.

# iLKke's mockups #
![http://grafx2.googlecode.com/svn/wiki/pictures/devdoc/layer_mocks.png](http://grafx2.googlecode.com/svn/wiki/pictures/devdoc/layer_mocks.png)

We spent some time with Ilija trying to tune up this. The horizontal strip seems more appropriate.

**Note on mockup:**
In the horizontal strip, some buttons have RMB functions: add+rmb=clone; merge+rmb=flatten (merge all)

# iLKke's ideas & thoughts #
These are provided here so you can all read them. The text can then be integrated with the rest in a more tidy manner. Excuse the formatting.

LAYER MENU

vertical:

> pros:

  * uses spare space
  * vertical layer display makes sense

> cons:

  * tiny buttons(1)
  * clutters the rest of the GUI if separators are removed(2)

horizontal:

> pros:

  * more space for buttons and overview, also for basic functions
  * would have to be done for animation anyhow

> cons:

  * takes up more screen space(3)

(1)tiny buttons can be countered by having an adaptive button size (as on mockup)

(2)use smaller separators (as on mockup)

(3)brilliance proved this to not be a real problem as long as you can hide/show all menus via keyboard

All in all, horizontal seems to work better.

THUMBNAIL PREVIEW (for horizontal menu only)

> cons:
  * takes up a lot of screen space
  * might prove unreadable most of the time, even at relatively large thumbnail sizes

> possible solutions:
  * a set of assignable icons/colors for layer buttons instead of thumbnails(1)
  * thumbnail preview only available in special layer popup/arranger(2)

(1) external data that would need to be saved somehow, also, active/hidden layers would have to be denoted using other means than color.

(2) will make a quick mockup of it at some point, but this is not ideal since it would be optimal to have all or most parts of layer GUI in one horizontal strip

ADDITIONAL LAYER OPERATIONS:

-move layer up/down - for arranging layers (already in mockup)

-flash current layer - for quickly identifying layer contents. can be a key shortcut, or optionally when you select a layer it would flash briefly (toggable in prefs). flashing would be changing the colors of the layer contents for a brief period of time, perhaps to black then white. perhaps someone has a less aggressive idea.
> UPDATE: optionally the layer could shake very briefly (move by a pixel vertically then back) or blink (go off/on) instead of the epilepsy-inducing flashing.

-load/save individual layers - quite useful. perhaps add optional merging of palettes, etc

Those last couple of features that haven't been included in the strip can be available by clicking on the 'layers' button on the left of the strip. Or included in the strip, somehow.

# Layer menu #

In any case, a "layer menu" button is not necessary, it can be replaced by double-clicking the active layer.

The "layer menu" can propose:
  * Set transparent color
  * Add empty layer
  * Clone current layer
  * Delete current layer
  * Flatten all

UPDATE:
> Functions that have dedicated buttons should be removed from the layer menu (all of the above?). Instead, two important functions could take their place:
    * Load layer
    * Save layer

The existing "Copy to spare" menu will behave differently if the spare is a multi-layer image:
  * The copy of pixels (choices 1,2 and 4) will copy current layer to (replace) spare's current layer, without changing the spare's dimensions.
  * "Palette and Remap" will remap all the layers of the spare.
This will be the method to import an image as a new layer: Add new layer, Swap to spare, load image, 'Copy to spare' / 'Pixels'.

I would really prefer using only one color index, of user's choice, as
transparent within the image. It will be transparent for us for all layers
except the last visible layer, where the color shows. I know it's traditional
for windows program to show a checkered pattern, but it's going to be slow for
us and it's equally traditional for sprite artists to draw on "magic pink" or
any color of the right luminance as the expected background that is clearly not
in their palette. The only drawback is all the layers are then 255 colors only.
Independantly from this, the user can still choose a "transparent color for GIF
or PNG".

Actually I was thinking of something more like the "Stencil" system we have,
but it would make the selected colors transparent, instead of not allowing you
to draw on them. But maybe it's overkill, if I want to make part of a drawing
appear and disappear in an animation I'll just put these part on a separate
layer, and make it invisible as a whole. So let's go for a single transparent
index.

### Shared layers ###
Optionally, with animation and layers, we could implement Shared layers.

A shared layer is a layer which is present in more than one step of the animation. A classic use is to make your background layer shared, so it is present in every step of animation, and drawing on it will affect all the steps at a time.

This system doesn't allow a layer that scrolls/pans as an animation... It would require a full recomputing of all frames every time you draw something, it's too slow to do it dynamically.

In terms of UI, we have to think a bit. The system can handle a lot of things, but it's not easy to make it clear and user-friendly.

For the implementation, it's rather easy because we'll already have reference-counting in place to handle backup steps. We only have to be careful when saving/loading, because it would automatically separate the layers on saving.

# Architecture overview #

Both layers and animations are part of the code refactoring. Animation things
will be made available in the gui later.

![http://grafx2.googlecode.com/svn/wiki/pictures/devdoc/pages_class_diagram.png](http://grafx2.googlecode.com/svn/wiki/pictures/devdoc/pages_class_diagram.png)

At the top you see the current system.
At the bottom it's the new one.

# Notes #
We introduce three new structures: T\_Timeline, T\_Frame, and T\_Layer, and we do
some changes in the T\_Page and T\_List\_of\_page.

## T\_Timeline ##
Its a linked list of T\_Frames, sorted by timestamp.
The T\_Timeline holds the comment, filename, format and directory of the current
edited file. It is possible to have only one T\_Frame, one T\_Layer and one T\_Page
to handle usual still picture files.

## T\_Frame ##
This holds the data for a frame: palette, timestamp, and a linked list of
layers. The palette is stored here because it needs to be global to the frame
(we allow 256 colors on screen at once, no more) and because this allows to
display the same page with different palettes for palette cycling.

Of course the list of layers is ordered by Z-Order, from bottom to top, this
allow easy rendering of the frame by simply rendering the layers in the order
they come in the list.

## T\_Layer ##
This is the struct defining a layer. It holds a pointer to the picture data (this
picture data can be used in multiple layers, in the same frame or in different
successive frames). It also holds the transparent color number (this one can
also be different for each occurence of the picture data) (maybe there should be
multiple transparent colors ?), and finally, the distorsion is handled there
simply by storing the screen pixel coordinates of the 4 corners of the layer.
This allow to render any kind of distorsion using only the linear\_distort
function we have for brushes. However, it's pretty hard to generate this data by
hand to make a proper rotation, so we will need a powerful way of generating
them. We may want to store the parameters used for this generator (lets say,
translation vector, rotation speed, zoom ratio, and simple offset for
hand-distorsion of each of the 4 corners), allow the user to tweak them at any
time to change his animation, then interpolate them to generate our distorsion
points. This would then be some kind of keyframe you place at main points of the
animation, while the other frames are interpolated from them.

## T\_Page ##
A T\_Page holds a bunch of pixels with the width and height. It can be packed
using some RLE and delta system to avoid wasting memory. However, I think all
pages used in the animation should be depacked before playing. This can be done
at the same time we generate interpolated frames from the keyframes, when you
click the "render and play" button. The packing is particularly interesting for
backup pages that, most of the time, are not used (particularly the old ones).
Actually, the delta only make sense in the backup list because this animation
system does not provide a way to have ordered pixel data to make an hand-drawn
animation. If you do that, it's just a set of frames with different pages of the
same size, the same palette, and the same distorsion everywhere. But the T\_Pages
don't know they are ordered in an animation. They can even be used in completely
unrelated places and without animation (or in reverse order) at another place.

As a T\_Page can be used in multiple layers, i think it makes sense to add some
simple reference counting mechanism. Each time an object get a pointer to a
page, it increments a counter. When the object is deleted or release its pointer
in any way, it decrements the counter. When the counter reaches 0 the page could
be deleted immediately. Or it could be kept in packed form in some kind of
pagelist, allowing to use it later in another layer. This is also used for
backups: when you backup a picture you only save the modified layer and copy the
references for all the others.

## T\_List\_of\_pages ##
This is used in the current backup system. I'm not sure how we should handle
undo/redo with the animation. We can have a separate undo list for each T\_Page,
or for each T\_Frame (allownig to undo any change including palette, distorsion).

If the backup list is a list of frame, then it is possible to undo frame
deletion, because we can push the frame back in the main list thanks to its
timestamp.

The way I see it, most editing actions modify only one layer of the current
frame. Some actions DO modify several or all frames, like for example a resize.
With a smart system of reference counting, we can point to the same pixel data
(T\_Page) for the different "editing steps" of layers that couldn't be affected
by the operation. I find this idea critically important for performances,
because on each action (brush stroke) we need to backup for the undo/redo
system, and not having to duplicate a dozen of frames is going to be a
lifesaver.

# Rendering, display to screen #
For the drawing, actually, we will have to have 3 things in memory:
  * The current layer
  * The rendering of all the other layers (both top and below)
  * A mask saying for each pixel in which layer it actually is. By testing this value against the current selected layer we can tell if the pixel is modifiable in a visible way or not. Storing the layer numbers in this plane allow us to keep it when the user go to another layer.

Remember that almost all effects need to read from the "backup page". For each
tool there is always the question if it should read from the last backup of
"only current layer (brush grab)", or "current layer and all visible layers
below it" (like smear, you smear under the top layers) or "all visible layers".

This is the most difficult thing to handle. Having it behave differently for
each tool seem uneasy to learn, having it as an option is too much buttons
(feeture creep as they say), and I think a single setting for all of them will
not make sense. One solution could be to take from all visible layers, and let
the user swich off the ones he don't want to use. But this means a lot of
playing with layers. Maybe a feature to store the current visibility of layer
and then restore it afterwards can do the trick. But, it's still not a perfect
workflow.

# File format #
We will have to design our own format to store all of this in a convenient form.
PKM can be extended for that using more/different chunks, not necessarily
keeping compatibility and name, but using the same chunk system. We will want to
import palette cycling from neochrome, degas elite, and IFF format, and to
save/load gif animations. Maybe we can find infos on what other animation
package such as Autodesk Animator Pro had (features, file format, ...)

## Use extensibility of PNG and GIF ##
PNG and GIF allow us to add custom chunks of data that will (should?) be ignored
by viewer programs. The files will be quite big, because we basically store all
the individual layers in addition to the "visible" flattened image.

## Rely on standard GIF behavior ##
For layers, one early/easier method is to use GIF to store layers as individual
frames with a delay of 0 and no repetition. In theory it's the ideal file format
as it has no size overhead, unfortunately many GIF viewers impose a minimum
delay of 1/10s or 1/20s (Firefox, IE), and some are unable to display a framed
GIF without repeating it in a loop. Still we can use it as an internal format.

Here's an example of such image:

![http://grafx2.googlecode.com/svn/wiki/pictures/devdoc/layers.gif](http://grafx2.googlecode.com/svn/wiki/pictures/devdoc/layers.gif)

Technically it's a 8-frame GIF. Frames are background, characters, GUI, Title, and 4 more unused (empty ones).
Dispose method is "do not dispose", and time of each frame is 0.05s. The NETSCAPE2.0 extension that requires looping
is NOT present, so it shouldn't loop.

This loads as a layered image in GIMP, so I guess using this format will make everyone happy. However, it does not show properly in geeqie (linux image viewer), only the first frame is there because they don't support animated gif. Opera 10 seems to show it fine.

## VGAPaint example ##

I launched vgapaint to see what it had. There are no layers. The animation is
bitmap-frame based, and the palette is handled a bit like what I did for pixel
data, ie a single palette can be shared between multiple frames, but you can
also decide to use another one. There is nothing much more to say. The function
to import a set of numbered PCX from hard drive looks interesting (load
ANIM0001.PCX as first frame, ANIM0002.PCX as second, and so on). There is sound
support (well... I think we don't need that), AVI import/export, and a custom
format, .VAN. I've uploaded a wiki page called [VGAPaintMenus](VGAPaintMenus.md) if you want to
have a look at it (just so it's linked from somewhere :p).

I had a look at the VAN file format. It's quite primitive actually. There is a
magic number, a small header with number of frames, framerate, width, height,
and palette, then each frame also starts with a magic number, a different one
depending on if there is a palette or not; there is the palette and the pixel
data ,either as RAW or RLE-encoded. So it's some kind of chunk based format but
does not sound as clean as our pkm (no size indication at begin of chunks, so no
way to skip a chunk). I also find VGAPaint's code less easy to read than ours...

# Use of animations #
Of course playing with animations is nice, but if they can't go out of the
program, it's of little interest. Gif export is already a nice solution, but the
ability to play your own format in another program directly would be really nice.

The idea is to provide a piece of code to render and play the animation in any
program using SDL. In this context, another program could ask us to render a
frame to an SDL screen, either with some content already in it, or just filled
with magic pink for blitting later. The frame render should not touch the unused
pixels, it should not fill the screen in black. It'd be really nice to be able
to control the engine and use it to build simple games (let it load all the
layers, but build the timeline in realtime depending on what the player does).
But maybe i'm dreaming too much :). Rendering over a 24bit screen could also be
a nice feature, in order to have a 24bit background and then simple layers in
256colors over it. Or a 3d game with some animation to make the ingame display.
But, let's start with simple things :)