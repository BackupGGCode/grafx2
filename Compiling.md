# Introduction #

If you're a linux user who needs to compile the program on his machine to run it, here are the instructions to do it. If you want to contribute to the development of GrafX2, here are more instructions to setup the development/packaging environment.

In either case, the building process uses **make** and the **gcc** C compiler, available under all linux variants and also on Windows (we're using MSYS and Mingw). Other OS or compilers may or may not work, with more or less modifications to the sourcecode. The makefile is able to compile the code on the following platforms :
  * Amiga OS 3 and 4
  * AROS
  * MorphOS
  * Various BSD flavours (NetBSD, OpenBSD, FreeBSD)
  * BeOS and Haiku OS
  * Linux (several distros)
  * SkyOS
  * Windows
  * Atari TOS/FreeMiNT
  * Mac OS X (including universal binary and app bundle support)

If you have got GrafX2 built on another system, please send us your patches to the source and project files. We will be happy to integrate them on the main source tree. When the project produces some very stable versions, it will be nice if some people can build RPM/Deb/... packages for the different linux distributions.

# Building GrafX2 #
## Requirements ##
### All platforms ###
  * GNU C compiler (gcc)
  * GNU make v3.80 minimum
  * SDL library v1.2
  * SDL\_image library
  * libpng
  * FreeType library (optional)
  * SDL\_ttf library (optional)
  * liblua5.1 (optional)

Note that some libraries have a package for the runtime, and a different package for the developer tools that are required to compile Grafx2: for example SDL will have "libsdl1.2-dev".

### Mac OS X ###
See [here](OSXBuildSetup.md)

### Windows only ###
  * a POSIX environment: MSYS is fine, maybe Cygwin would work as well.
  * the MinGW C compiler (this replaces gcc) Version 3.4.2 is known to work.

### Generic UNIX only (Linux, FreeBSD, ?) ###
  * pkg-config if you want to include lua support

On debian-based distributils you should be able to get all these files by simply running trhe following command from a terminal :
```
sudo aptitude install gcc make libsdl1.2-dev libsdl-image1.2-dev libsdl-ttf2.0-dev libfreetype6-dev liblua5.1-0-dev lua5.1
```

### Atari TOS/FreeMiNT ###
The Atari build is very similar to the Linux one. The build might work on native machine with gcc 4.3> compiler, but it wasn't tested. You can also build binary for Coldfire based machines(e.g. Firebee) by
replacing '-m68020-60' in makefile with '-mcpu=5475'(you can use '-mcfv4e' too, but this option may be deprecated in future versions of gcc, so '-mcpu=5475' is more favourable).

Preferable way is to build GrafX2 with use of cross compiler, you can get one from [Vincent Rivière site](http://vincent.riviere.free.fr/soft/m68k-atari-mint)(URL: http://vincent.riviere.free.fr/soft/m68k-atari-mint). There are versions for win32 (Cygwin) and debian packages for latest Ubuntu (32/64bit).

Before compilation you have to build all the needed libraries mentioned in requirements.

To compile a Atari TOS executable, type in
```
	make ATARICROSS=1 prefix=/usr/m68k-atari-mint
```
You can also add other options like NOTTF, NOLUA, NOLAYERS etc. to enable/disable program features..

If you don't know how build libraries here's some hints. Please note that prefix path in examples below is valid only under Linux,
in case of Cygwin the path will be '/opt/m68k-atari-mint'. There will be no prefix when building on native machine.
You have to omit 'sudo' under Cygwin and native build. Stick to this order and you will be fine ;> ...
The versions of libraries were tested, you can also try newer versions. As I mentioned earlier, replace '-m68020-60' with '-mcpu=5475'
if you want to target Coldfire machines.

#### libpng (optional, for png reading in SDL\_image) ####
##### note: you will need libzip too #####
libpng 1.2.44
```
./configure --prefix=/usr/m68k-atari-mint --disable-shared --enable-static --host=m68k-atari-mint CFLAGS="-m68020-60 -O2 -fomit-frame-pointer"
sudo make install
```
or
libpng 1.4.44
```
./configure --prefix=/usr/m68k-atari-mint --disable-shared --enable-static --host=m68k-atari-mint CFLAGS="-m68020-60 -O2 -fomit-frame-pointer -DPNG_NO_SETJMP"
sudo make install
```

#### libjpeg, libtiff (optional, for jpeg/tiff support in SDL\_image) ####
```
./configure --prefix=/usr/m68k-atari-mint --disable-shared --enable-static --host=m68k-atari-mint CFLAGS="-m68020-60 -O2 -fomit-frame-pointer"
sudo make install
```

#### freetype 2.4.4 (optional, for TTF fonts support, required by SDL\_ttf) ####
```
./configure --prefix=/usr/m68k-atari-mint --disable-shared --enable-static --host=m68k-atari-mint CFLAGS="-m68020-60 -O2 -fomit-frame-pointer" 
sudo make install 
```

#### lua 5.0.4 (optional, for LUA scripting support) ####
Here you have to customize makefiles, add prefixes, platform has to be set as generic.

#### SDL 1.2 (mandatory) ####
##### note: best is to grab it directly from Mercurial repository #####
```
./configure --prefix=/usr/m68k-atari-mint --disable-shared --enable-static --host=m68k-atari-mint --disable-video-opengl --disable-shared --enable-static --disable-threads CFLAGS="-m68020-60 -O2 -fomit-frame-pointer"
sudo make install 
```

#### SDL\_ttf (optional, for ttf fonts support, depends on SDL and freetype) ####
```
./configure --prefix=/usr/m68k-atari-mint --disable-shared --enable-static --host=m68k-atari-mint --disable-shared --enable-static --with-sdl-prefix=/usr/m68k-atari-mint --with-freetype-prefix=/usr/m68k-atari-mint CFLAGS=" -m68020-60 -O2 -fomit-frame-pointer"
sudo make install 
```

#### SDL\_image 1.2.10 (mandatory) ####
```
./configure --prefix=/usr/m68k-atari-mint --disable-shared --enable-static --host=m68k-atari-mint --disable-shared --enable-static --with-sdl-prefix=/usr/m68k-atari-mint CFLAGS="-DHAVE_OPENGL=0 -m68020-60 -O2 -fomit-frame-pointer"
sudo make install 
```

## Instructions ##
Open a shell/Terminal, cd to the directory where you have the sourcecode, and type `make`.
If all goes well, it should build **grafx2** in the current directory. Voilà.

### Buildtime settings ###

If you don't have FreeType and SDL\_ttf, type `make NOTTF=1` instead. It will build a version without TrueType support : the Text tool will be limited to bitmap fonts, proportional fonts wiht .ttf extension won't be available.

If you don't have lua available, type `make NOLUA=1`. You will not be able to use lua scripts to generate and alter brush and pictures.

These options can be combined, for example for a build without ttf nor lua type `make NOTTF=1 NOLUA=1`.

Under linux, you can then run `make install` to get the files installed in your system, in the /usr/local/ and /usr/share directories (the usual UNIX way). This may or may not work, the installation needs some more testing. Since these targets are system directories, it will require root priviledges.

If libpng isn't available for your platform, and you desperately need a version of Grafx2 even without PNG support, you can try compiling grafx2 without it. This requires modifying the makefile:  Locate the line `COPT =` for your platform, and add -Dno\_pnglib as one of the options. Locate the line `LOPT =` for your platform, and remove `-lpng` so that it no longer attempts to link with the library. When the executable successfully compiles, you'll still have to convert any resource that grafx2 uses at runtime (like the default skin) from PNG format to GIF format. You can still keep the file extensions in ".png", so that that the code that refers to the file doesn't need to be updated.

## Problems ##
### If Make complains about a missing `Makefile.dep` ###
We forgot the file in some source archive of the early betas (2008). Fortunately, it's a file you can re-generate:
  1. Edit the Makefile. Find a line that reads _include Makefile.dep_, and put a # before it to comment it.
  1. Run make with the "depend" argument: `make depend`
  1. Edit the Makefile again, and remove the # sign.
  1. Run `make`
### (Windows) SDL.h: No such file or directory ###
Apparently the automatic installation of SDL headers does not work very well under windows if you put them in MSYS's own root.

In a MSYS shell, run `which sdl-config`

It will tell you where the sdl-config script is located, for example:
/usr/bin/sdl-config

Edit this file in vi or any text editor to see where SDL believe it's installed.

If one line says `prefix=/` you have installed SDL in MSYS's directories (headers in `<msys root>/include/SDL` and library in `<msys root>/libs`) and it doesn't work under Windows, you need to change the config line so it says `prefix=/usr` or `prefix=` and it will work correctly.
Headers and libs for SDL\_image and SDL\_ttf should be stored in the same directories as SDL.
### Makefile:nn: Extraneous text after `else' directive ###
This fatal error is due to using a version of `make` earlier than v3.80.
Type `make --v` to check your version.
Note that on windows, depending on your installation you may have /bin/make.exe and also /mingw/bin/mingw32-make.exe
# Developers: Building variations #
You can use `make clean` to remove the intermediate generated files (.o) and binary.

You can use `make depend` to rebuild the dependency file Makefile.dep : Don't hesistate to rebuild it whenever you add some #includes "something.h", it will help the Makefile determine very accurately which files need to be recompiled when something.h is modified. And svn is smart enough to see if the file is actually changed or not before increasing the version.

The current compilation options are -W -Wall that warn of most common mistakes, -O for a basic level of optimization like omitting dead code and collapsing identical constants, and -ggdb to generate debug information for the GNU debugger.
As of version 2.3, Grafx2 compiles with normally zero warnings.

You can compile with `make OPTIM=0` to disable otimizations for easier debugging. It controls the -O`<n>` setting for GCC, where `<n>` is either blank, 0, 1, 2 or 3. blank has the same effect as 1, so OPTIM= and OPTIM=1 are identical and give the same result as when you don't specify it.

You can use `make release` to strip the debugging information.

You can use `make version` to check the state of the current directory and store the result in a constant string in version.c. This file is used during normal compilation, it's how the program can display a SVN revision number in the About/Stats screen.
This command requires the Subversion product. It's mostly useful for packagers (see the relevant section), but you can use in your own builds as well.

# Developers: Source code management #
googlecode.com hosts our Subversion (svn) repository
To access it, you need to have a Subversion client installed.
Then check the instructions on http://code.google.com/p/grafx2/source/checkout to download a copy of the sources.
If you have the command-line version of svn, the typical commands are:
  * svn status : Check the differences between your version and the latest
  * svn update : Import/merge the latest changes into your copy
  * svn revert _file_ : Reload the server's version of _file_
  * svn commit : Send your changes to the server, as a new revision. (requires write access)
Be careful that googlecode's SVN does not allow anyone to undo something, changes can only go forward. So, check everything twice before commiting something.
The repository is readonly for unregistered users, if you want to contribute, contact us and we'll be happy to add your login to the project members.

# Developers: Packaging a version #
There are facilities to package the source and binary versions, using the Makefile. They'll work for all platforms, but you need some extra tools:
  * tar
  * gzip
  * zip (If your distribution doesn't have it, find it at http://www.info-zip.org/)
  * svnversion (installed with subversion)

The packages are numbered according to the svn revision of their contents, so you should start from a clean state regarding svn, ie: When you type `svn status`, no file should appear modified/added/deleted from the revision you're packaging. Try to do an `svn commit` then `svn up` to ensure everything is ok.

Type `make ziprelease`
After a few seconds, you should obtain in the current directory:
  * **grafx2-svn000-src.tgz** : Data, docs, sources
  * **grafx2-svn000-platform.zip** : Data, docs, sources (in an embedded `src-svn000.tgz` file)
platform will be replaced by the name of your platform, such as reported by the `uname` command if it does exist, or as you specified it in the makefile.
000 will be replaced by the svn revision number, such as:
456 : revision number 456, clean.
821M: revision number 821, but with more changes on your part that the server doesn't have.
In the second case, it's probably a bad idea to release the package... Commit your changes before to avoid letting us with hundred of slightly different versions floating around.

The `ziprelease` target ensures that the same revision number will appear:
  1. In the filename of the sources zip
  1. In the filename of the binary zip
  1. In the filename of the source-only archive (inside the binary one)
  1. When you run the executable from the binary zip
  1. When you re-compile from either source archive, and run the executable.

If you add the NOTTF=1 argument, the archives have the additional suffix -nottf.

# Developers: Uploading a version #
The project page can host downloads:
http://code.google.com/p/grafx2/downloads/list
It's extremely important to think twice before uploading, because googlecode is write-only: even the project owner cannot rename or delete a file. The most he can do is remove it from the front page, but it's still in the public archives.

# Building under Windows with Open Watcom #
This is no longer supported. Please read an older revision of this Wiki page if you desperately need the info. It may not work with the most current versions of the sourcecode, anyways. The project file is still in the subversion, but it is outdated (missing some new files). You'll probably find that Open Watcom's C compiler will throw errors in some places where gcc doesn't. Good luck with that.