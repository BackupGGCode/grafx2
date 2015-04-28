# Configuration files #

GrafX2 uses two files to store its configuration: 'GFX2.INI' and 'GFX2.CFG'.
## Where ? ##
On Linux and similar, they are stored in the hidden directory `$(HOME)/.Grafx2`

On Windows, starting from Windows NT/2000, open an explorer and type in its address bar `%APPDATA%\Grafx2` to reach the directory where they are stored. The actual directory depends on your version of Windows, it can be for example `C:\Documents and Settings\username\Application data\GrafX2` (Windows XP), and `C:\Users\username\AppData\Roaming\GrafX2` (Windows Vista).

On Mac OsX, the files are in ~/Library/Preferences/com.googlecode.grafx2 .

On GP2X, Windows 98, and Amiga-like systems, the settings are always kept in the same directory as the program.

Note that the standard locations above are for a normal, "user" installation of grafx2. The behavior of the program is to first search the file in its own directory, and use them there (read and write) if it finds them. This allows several cases:
  * Installing two versions of Grafx2 side-by-side, for example the latest stable and the latest WIP, without sharing the configurations : Install the program in a place where your account is allowed to write, and put a copy of the configuration files there.
  * (Windows at least) Putting GrafX2 on a USB memory stick, with its configuration files, so you can plug it in any PC and start drawing, without having to install anything or leaving any trace on the PC !

## GFX2.INI ##

This file contains the parameters defined in the settings menu and some others. You may edit this file with any standard ASCII editor. When you click on Reload in the settings menu, all the data contained in this file are restored. When you click on Save or when you quit the program with the Auto-save option on, all the current parameters are written into (updated in) this file.

If you corrupted this file and don't manage to fix the problem, then delete it and run grafx2 again. It will automatically create a default initialization file when it is absent.


## GFX2.CFG ##

This file contains the keyboard configuration plus the state of the following variables in the program:
  * video modes
  * shade tables
  * stencil
  * mask
  * gradients

All these variables are saved when clicking on the Save button in the settings menu or when exiting the program with the Auto-save option on. However, when you click on Reload in the settings menu, only the state of each video mode is restored.

Note: the GFX2\_FRA.CFG file is a default configuration file for AZERTY keyboards. If you have got an AZERTY keyboard, you may replace the GFX2.CFG file by GFX2\_FRA.CFG.

Important: from version 2.00 ß95.5% to 96.5%, .CFG files will have ascending compatibility. This means that you'll be able to retrieve most of their contents from a release to another by copying your old .CFG file into your new GrafX2 directory and running grafx2. Indeed, the program will convert your old file for it is usable by the new version of GrafX2. But copying a .CFG file from an earlier version than version 95.5% won't work. Moreover, (I don't see why you would do that, but...) copying a recent .CFG file to an older version shouldn't work neither.

From version 97.0%, the compatibility is handled directly in the main program, you don't have to run an external utility called GFXCFG to get your files converted. However, this was tested only with files coming from the 96.5% version. If you have a configuration file from an older version, it is recommended that you open it with 96.5% GFXCFG.EXE, before using it with newer versions.