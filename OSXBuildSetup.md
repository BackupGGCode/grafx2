# Introduction #

The Mac OS X build process is not that simple. It's hard to get it right and get something that will work everywhere.

# The correct approach : Frameworks #
Get and install the dependancies :
  * SDL : http://www.libsdl.org/release/SDL-1.2.14.dmg
  * SDL\_image : http://www.libsdl.org/projects/SDL_image/release/SDL_image-1.2.10.dmg
  * lua : http://www.malcolmhardie.com/opensource/LuaFramework/index.html
  * libpng : http://ethan.tira-thompson.com/Mac_OS_X_Ports_files/libpng%20(universal).dmg

You need to install xcode to get the developer tools.
Then, edit the makefile to setup the arch and framework directory (near the top of the file) : MACOSX\_SYSROOT and MACOSX\_ARCH.

Then proceed as usual by running make.

**warning : this seems to create non-working binaries right now.**

# Using macports #

Macports works like a linux package management system. You can use the resulting binary on your computer, but it is not self-contained, so you can't use it elsewhere, unless you also install the macports stuff.

For now you need to comment framework stuff in the makefile and uncomment macport stuff (4 lines about SDLCOPT, LUACOPT, SDLLOPT, LUALOPT) ; and comment the equivalent framework-based ones.

Proceed with the "generic unix" instructions.