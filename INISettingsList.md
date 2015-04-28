The goal is to get a list of settings that can't be changed from the GUI. If we add them all, it is possible to remove comments from the inifile and use a proper ini handling library.

  * OK = Setting is accessible from the GUI
  * DEL = Setting is unused, drop it
  * ADD = Setting is not in GUI, add it

# Mouse #
|Setting|Status|Notes|
|:------|:-----|:----|
|X\_Sensivity|OK|In settings screen|
|Y\_Sensivity|OK|In settings screen|
|X\_correction\_factor|DEL|  |
|Y\_correction\_factor|DEL|  |
|Cursor\_aspect|OK|In skin screen|

# Menu #
|Light\_color|DEL|Loaded from skin|
|:-----------|:--|:---------------|
|Dark\_color|DEL|Loaded from skin|
|Menu\_ratio|ADD|  |

# File selecor #
|Show\_hidden\_files|OK||
|:------------------|:-|:|
|Show\_hidden\_dirs|OK|  |
|Preview\_delay|ADD|  |
|Maximize\_preview|ADD|  |
|Find\_file\_fast|ADD|  |

# Loading #
|Auto\_set\_res|OK||
|:-------------|:-|:|
|Set\_resolution\_according\_to|ADD|Might be done as a dropdown replacing auto-set|
|Clear\_palette|ok|

# Misc #
|Draw\_limits|ok||
|:-----------|:-|:|
|Adjust brush pick|ok|  |
|coordinates|ok|  |
|backup|ok|  |
|undo\_pages|ok|  |
|gauges scrolling speed\_left|ADD|  |
|gauges scrolling speed\_right|ADD|  |
|auto-save|OK|  |
|Vertices\_per\_polygon|ADD|  |
|Fast\_zoom|ADD|  |
|Separate\_colors|OK|  |
|FX\_Feedback|OK|  |
|Safety\_colors|OK|  |
|Opening\_message|ADD|  |
|Clear\_with\_stencil|ADD|Should be an option in the stencil menu ?|
|Auto\_discontinuous|ADD|  |
|Save\_screen\_size\_in\_GIF|ADD|  |
|Auto\_nb\_colors\_used|ADD|Needs to be on for the histogram feature to work|
|Default\_video\_mode|OK|  |
|Default\_window\_size|OK|  |
|Merge\_movement|ADD|Should not be needed anymore if we switch to a proper event driven input system|
|Palette\_cells\_XY|OK|  |
|Bookmarks|OK|Can't use the same name for all of them. Should switch to bookmark1**|**|Palette\_vertical|OK|  |
|Windows\_position|OK|  |
|Double\_click\_speed|ADD|  |
|Double\_key\_speed|ADD|  |
|Skin,Font|OK|  |
|Grid\_XOR\_Color|ADD|Should be part of the grid setting menu; or in palette settings and used for all XOR ops|