# Introduction #

You can launch Grafx2 with some command line arguments to open a file directly or get a specific option. Note that on Windows, drag-and-dropping a file on a Grafx2 shortcut will pass the file name as the only command-line argument, so it will start Grafx2 with this file loaded.

# List #

  * **/?** displays help, along with a list of the availables videomodes. Ex:
```
Syntax: grafx2 [<arguments>] [<picture1>] [<picture2>]

<arguments> can be:]
        -? -h -H -help    for this help screen
        -wide             to emulate a video mode with wide pixels (2x1)
        -tall             to emulate a video mode with tall pixels (1x2)
        -double           to emulate a video mode with double pixels (2x2)
        -wide2            to emulate a video mode with double wide pixels (4x2)
        -tall2            to emulate a video mode with double tall pixels (2x4)
        -triple           to emulate a video mode with triple pixels (3x3)
        -quadruple        to emulate a video mode with quadruple pixels (4x4)
        -rgb n            to reduce RGB precision from 256 to n levels
        -skin <filename>  to use an alternate file with the menu graphics
        -mode <videomode> to set a video mode
Arguments can be prefixed either by / - or --
They can also be abbreviated.

Available video modes:

      window     320x200     320x240     320x256     320x400     320x480
     512x264     512x288     576x240     592x240     608x240     632x264
     704x288     736x240     768x240     768x288     784x240     800x288
    1280x960   1280x1024    1360x768    1600x900   1600x1024   1600x1200
```
  * **/mode 320x200** starts grafx2 in 320x200 fullscreen video mode. All modes are fullscreen except for the special name "window".

  * **/double** emulates 2x2 pixels, **/triple** emulates 3x3 pixels, **/quadruple** 4x4 pixels. These are useful when the intended display resolution of your picture (eg for 320x240) is much greater than the actual resolution of the display you are editing it on (eg 1280x960), and/or the GUI of Grafx2 is becoming too small / unreadable.
  * **/wide** and **/tall** allow to use rectangle pixels (horizontal and vertical). This is useful to edit Amstrad CPC pictures, for example.
  * **/wide2** and **/tall2** are doubled versions of /wide and /tall. That is, /wide2 uses 4x2 pixels, and /tall2 uses 2x4 pixels.
  * **/rgb n** sets the color depth to n. For example, /rgb 2 will give you a spectrum-style 16-colors palette, /rgb 3 will give the Amstrad CPC 27 colors, /rgb 16 will give a classical Amiga palette, and /rgb 64 will give you a VGA palette, like the DOS version of grafx2 had.
  * **picture1** and **picture2** are the names of files to open immediately.

For example :
` grafx2 /mode 320x200 My_drawing.png`