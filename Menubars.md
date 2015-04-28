# Introduction #

GrafX2 uses a single menu with all the tools inside. This is great, but we're running out of space and we need to add more features. As we don't want to have a menu that eats up the whole screen, and features that stay hidden if you don't want to hear about it, we need to improve the menu system to have separate bars with different tools inside.

# Bars #
Planned bars for now :
  1. Status bar : Always at the bottom of the screen. Display the status text and the "bars" button.
  1. Drawing bar : The one you know. Buttons for drawing, for advanced tools, load, save, settings, and all that stuff.
  1. Layer bar : Displayed between drawing and status. Layers and layers operations
  1. Animation bar : Displayed above or below the drawing bar ? or below the layers ? Tools for animation, timeline, and this kind of stuff.
  1. Effects bar : above drawing bar. May replace the effects window. But it may not be worth it, you loose screen space and do you really win something ?

# Handling #

Bars are in a static order. They can't be moved. But you can hide or show them. To do that, the "hide" button in the statusbar will be replaced with a "bars" button, opening a small popup menu ((see mockups in the page about layers and animation for now). The menu allows you to select a bar, then the status of this bar is switched.

F10 still hides everything, or show things in the state they were before you hidden them. It is the only way to hide the status bar.

The drawing bar may or may not be hidden. It may be convenient to switch between "drawing" and "animation", one showing when you hide the other.

Other shortcuts may be used to toggle bars independantly (for example shift + F10 = toggle layerbar, ctrl+F10 = toggle animation/drawing, ...).

In the mockups, bars only expand to the part used by the menu, letting the palette area free. The palette may use this vertical space, or we could put something else in there. Or we could have the bar use full screen width, and the palette included in the drawing bar. This seems to make sense.

Some bars, especially animation bar with timeline, would need all the horizontal space they can possibly get, leading to the idea of full-length bars. The problem this imposes is that the screen/window width is variable. Instead of stretching the interface, causing clumsy button sizes ad skinning issues, a better solution seems to center the bar horizontally, filling the remaining space with a (skinnable) tiling pattern.

Furthermore, if the layers bar used full menu width, more layers could be crammed in, or at least we could have a more ideal button size.

All in all, it seems that full-length makes more sense, even in this early stages.

# On the coding side #
Miscelaneous notes for implementation...
  * There is no way to have a dropdown button in the statusbar with the current code (buttons in the menu are not the same as button in windows). There is an experimental "popup" code but it does not work perfectly yet.
  * The "hide" button is handled as being part of the menu bar while actually it isn't. meaning if you move the drawing bar up to make space for the layer bar, the hide button will be in the layerbar instead of the statusbar.
  * The F10 key is plugged to the Hide\_menu button. It should not be moved to the "Bars" button. The Hide button should be moved inside the popup opened by the bars button (and be labelled "hide all").
  * If we want to get a nice popup like in the mockups, we have to make it skinnable. It uses smaller text and nice icons.
  * We have to keep track of the status of each bar, and also of the global status of the menu (F10). The menu can be handled as a special case : if the statusbar is hidden, don't show any of the other bars.
  * Have a table of bars. Struct bar may hold infos like
    * Bar height (this replace MENU\_HEIGHT)
    * Bar status (visible/hidden)
    * Pixel data of the bar (as loaded from skin)
  * The bars would be stored in this table in order, from bottom to top. So bar[0](0.md) is status bar, bar[1](1.md) is layers, bar[2](2.md) is menu.
  * Functions for guessing button number on menuclick need to take the bar status into account.
  * Menu\_Height is a variable and tells the total height of the menu. It is chaged each time you add/remove a bar. It is 0 when everything is hidden, so on showing back it needs to be recomputed (or saved somewhere). This is done so everything else does not have to check for Menu\_is\_visible.
  * Menu\_Y is a "mirror" of Menu\_Height. It is here only for performance puprose (avoids calculation of Screen\_Height - Menu\_Height). We need it in quite a lot of operations. Keep it in sync each time you touch Menu\_Height.