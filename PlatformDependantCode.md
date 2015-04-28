# Introduction #
How to code in GrafX2 for one platform without breaking the others.

# List of platforms #
  * Amiga OS3 and 4, AROS, MorphOS
  * BeOS and Haiku
  * gp2x
  * Linux
  * MacOSX
  * Win32 refers to versions of Windows : 98, NT, 2000, XP, Vista.

# Symbols table for detection #

|#ifdef|Linux|Win32 (MinGW)|Win32 (Watcom)|MacOSX|Amiga OS4|Beos|Haiku|AROS|MorphOS|FreeBSD|GP2X|Wiz|Caanoo|AmigaOS 3|
|:-----|:----|:------------|:-------------|:-----|:--------|:---|:----|:---|:------|:------|:---|:--|:-----|:--------|
|`__WIN32__`   |  |X | X |  |  |  |  |  |  |  |   |  |  |  |
|`__MINGW32__` |  |X |   |  |  |  |  |  |  |  |   |  |  |  |
|`__WATCOMC__` |  |  | X |  |  |  |  |  |  |  |   |  |  |  |
|`__linux__`   |X |  |   | X|  |  |  |  |  |  | X |X |X |  |
|`__macosx__`  |  |  |   | X|  |  |  |  |  |  |   |  |  |  |
|`__amigaos4__`|  |  |   |  | X|  |  |  |  |  |   |  |  |  |
|`__BEOS__`    |  |  |   |  |  | X|  |  |  |  |   |  |  |  |
|`__HAIKU__`   |  |  |   |  |  |  | X|  |  |  |   |  |  |  |
|`__AROS__`    |  |  |   |  |  |  |  |X |  |  |   |  |  |  |
|`__MORPHOS__` |  |  |   |  |  |  |  |  |X |  |   |  |  |  |
|`__FreeBSD__` |  |  |   |  |  |  |  |  |  |X |   |  |  |  |
|`__GP2X__`    |  |  |   |  |  |  |  |  |  |  | X |  |  |  |
|`__WIZ__`     |  |  |   |  |  |  |  |  |  |  |   |X |  |  |
|`__CAANOO__`  |  |  |   |  |  |  |  |  |  |  |   |  |X |  |
|`__amigaos__` |  |  |   |  |  |  |  |  |  |  |   |  |  |X |

Generally, you should assume a globally "unix" platform, and only put code in #ifdef block when you need to do something different for one platform.

Be careful that `__linux__` applies to MacOSX as well.

If you need to code a complicated kind of "switch", the cleanest way to write it would be:
```
#if defined(__BEOS__)||defined(__HAIKU__)
  // put BeOS/Haiku-specific code here
#elif defined(__amigaos4__)
  // put OS4-specific code
#else
  // put default alternative code here
#endif
```

# System-specific #
## Windows ##
Environment variable: **COMSPEC**. This holds the path to the command interpreter (ex: C:\CMD.COM) The Makefile uses this variable to detect Windows build. Hopefully nobody sets it in an other system.

Environment variable: **WINDIR**. This holds the path to the windows drive and directory (ex: C:\WINDOWS). Used to find fonts.
Directory separator: Windows filesystems traditionally use the character \ as a separator between directories, however / is also supported in **almost** all file i/o functions, and must be expected too.

Drives: An absolute file name begins with a drive name, from "A:" to "Z:". It is followed by a path separator, ex: "C:\GrafX2\gfx2.ini"

## Amiga-like systems (AmigaOS 3 and 4, AROS, MorphOS ##
Drives: AmigaOS filesystem has volume/drive name. It can be a "technical" name like "df0:" for Disk Floppy drive 0, or a user-set name like "games:". The volume or drive is **not** followed by a path separator, ex: "mp3:Switchblade Symphony/Clown.mp3". This means that a directory name can be "something:", with no trailing slash. The parent directory is /, not .. like on other systems.

Compiler: The compiler is VBCC, it doesn't support GNU extensions like `__attribute__`

# Caanoo specifics #

It seems the build will be little-endian.
Be careful to pick **signed** chars by default. If you make a mistake, some compiler warnings about "comparison always true" may be a sign.

# Endianness #

SDL already provides reliable macros to determine the host system's endianness (Big-Endian like PowerPC, or Little-Endian like Intel)
The syntax is
```
#if SDL_BYTEORDER == SDL_LIL_ENDIAN

#if SDL_BYTEORDER == SDL_BIG_ENDIAN
```
In general you shouldn't use them anyway. The most frequent reason you need to know endianness is when you read or write data to disk, and all the necessary functions have been coded in io.c, in two forms : big-endian (_`Read_word_be()`_) and little-endian (_`Read_word_le()`_). Just choose the functions that have the right endianness for the **file format** (ex:GIF is little-endian, LBM is big-endian), and the functions will perform swapping as necessary.

# Struct packing #

Structs in C are not guaranteed to be contiguous in memory, the compiler can insert dummy bytes between struct members in order to align the members on 2-byte, 4-byte or 8-byte addresses. In some cases it makes the program run faster (x86). In some other cases it's **mandatory** to access the members at all (Sparc, and ARM-based machines like the Caanoo).

The default behavior of Watcom C was to pack structures (Original code from 1996)
**The default behavior of gcc on x86 is to pad them**, so 2-byte data is on address multiple of 2, 4-byte data is on addresses multiple of 4, and the total structure has a final padding at the end, according to its biggest member.

As you can guess, when porting grafx2 we ran right into this one. An early fix was to pack a lot of structures by marking them with an GCC extension attribute: `__attribute__((__packed__))` or the `#pragma pack` (Which **is** supported on all versions of GCC that are currently in use).
Since then, to support big-endian cpus, all datatypes of more than one byte had to be handled individually for endianness anyway, the code now loads/saves them as individuel fread() and fwrite(), and thus the program no longer relies on having the structures packed.

As of 11/2010, only two structures remain forcibly packed: the RGB triplet T\_Components, and (as a consequence) the array of 256 of them: T\_Palette. This struct is only made of 8-bit types, so it can be packed on all platforms:
sizeof(T\_Components) == 3 and sizeof(T\_Palette) == 768.
The guideline now is to never write another structure that require packing. **Don't expect specific sizeof() values. Don't rely on sizeof() to automatically count the "file size" of a structure, even a packed one.** It just doesn't **always** work.
(You can still rely on sizeof() for memory allocation)

# Memory alignment #

On the Caanoo with its ARM architecture, you can't read a 2-byte number at an address that isn't a multiple of 2, and you can't read a 4-byte number at an address that isn't a multiple of 4. This has consequences on struct packing (see above), so for example the compiler will sometimes add padding **even if you use attribute or pragma to disable it**, without any compilation warning.

Also, you can trigger this problem if you try to cast a void pointer to a `word*` or `dword*` : The address will be rounded, or maybe the bytes will be shuffled (not clear at this moment).

The typical pitfall is trying to read a RGB triplet in a 24bit bitmap as a single dword fetch. **On all platforms, don't do that**. It breaks the Caanoo port.

# Zero-sized arrays #

Zero-sized array at the end of a struct, in order to support dynamic-allocated array: Use `elem[0]` on GCC v2 or earlier, `elem[]` on GCC >= 3 and any other compiler (including VBCC):

```
#if __GNUC__ < 3
  // gcc2 doesn't suport [], but supports [0] which does the same thing.
  T_Image    Image[0];  ///< Pixel data for the (first layer of) image.
#else
  T_Image    Image[];  ///< Pixel data for the (first layer of) image.
#endif
```

# Unused arguments #

The GCC-ism `__attribute__((unused))` breaks the compilation on Amiga-like platforms that use the VBCC compiler.
`__attribute__` should only be used when `__GNUC__` is defined. For unused arguments, in order to avoid a compilation warning, the following syntax works on all known platforms:
```
  (void)color; // unused
```
It can be surrounded by #ifdef in order to isolate the specific case when this argument is unused.

# Make dependencies #

In release source packages, the dependency file (Makefile.dep) is packed with the sources, and may be used on a different platform than the one where it was generated.
When this file is not up-to-date, you can get strange compilation or run-time time errors, that disappear only when you `make clean` and then `make`.
To keep everybody happy, running **make depend** should generate an identical file on all platforms. It's not difficult, you only have to avoid including some grafx2 headers conditionally:
```
#ifdef __WIN32__
#include "gfx2win.h" // bad
#endif
```
If you have such situation where there is source file that is not needed for all platforms ("gfx2win.c"), include the header always, and _in the header file itself_, enclose all the declarations in a conditional #if.

# 32bit vs 64bit #
Size of native types for C compiler:

**32bit compiler**
| **Type** | **Size** |
|:---------|:---------|
| short int | 16bit |
| int | 32bit |
| long | 32bit |

**64bit compiler**
| **Type** | **Size** |
|:---------|:---------|
| short | 16bit |
| int | 32bit |
| long | 64bit |