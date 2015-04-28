# Introduction #

Grafx2 under DOS has support for various file formats from other drawing tools. Each format's saving and loading routines have been rewritten to support the format on all platforms, with big-endian or little-endian CPU, and with no problems of byte alignment.
Here is a table showing the status of each format.

# Supported formats table #

| **Extension** | **Save** | **Load** | **Misc** |
|:--------------|:---------|:---------|:---------|
| GIF | Yes| Yes | Compuserve GIF 89a. Only one palette is supported, so high-color tricks are not supported. Transparent ("background") color is supported in load and save. Saving is always in 8-bit mode (256 colors). Layers are implemented as a non-looping animation. Since v2.4, animation is fully supported, be sure to use frame times in 1/100th seconds since it's the GIF precision. This format can preserve color cycling data. |
| PNG | Yes | Yes | Portable Network Graphics. Reads all forms of paletted images (from 2 to 256 colors), greyscale (any depth, converted to a 256-level greyscale palette from black to white). Additional PNG information, like Alpha channel and Transparency are not preserved. The image description is read and saved as the 'Title' text, limited to 32 characters. Saving is always with 256-color palette. Palette transparency is supported, up to 1 color can be fully transparent. Saving is always in 8-bit mode (256 colors) |
| PBM | Yes | Yes | 256-color format used by Deluxe Paint 2E (MS-DOS) and Deluxe Paint 3.5 and later (Amiga). This format can preserve color cycling data. |
| [LBM](http://en.wikipedia.org/wiki/ILBM) | Yes | Most | InterLeaved BitMap. Format used by all the Amiga versions of Deluxe Paint for bitplane-based images. Grafx2 can load all of them (including [EHB](http://en.wikipedia.org/wiki/Extra_Half-Brite)), but saving will auto-detect the used colors to determine if it should save 2, 4, 8, 16, 32, 64, 128 or 256-colors. A re-saved EHB image will become a normal 64-color image, not usable on OCS Amiga. This format can preserve color cycling data. |
| BMP | Yes | Most | Microsoft Paint. Some variants of Bitmaps cannot be loaded, neither by the original GrafX2 nor by our version. Saving is always in 8-bit mode (256 colors) |
| PCX | Yes | Yes | Z-Soft |
| IMG | Yes | Yes | Bivas (W. Wiedmann) |
| [PKM](PKMSpec.md) | Yes | Yes | Grafx2's original format. This is mostly preserved for historical purposes, this format has basic RLE compression but doesn't support layers or animation. |
| SC? | Yes | Yes | Colorix |
| [PI1](AtariFileFormats.md) | Yes | Yes | Degas Elite |
| [PC1](AtariFileFormats.md) | Yes | Yes | Degas Elite |
| CEL | Yes | Yes | K.O.S. (KISekae Set System) |
| KCF | Yes | Yes | K.O.S. (KISekae Set System) |
| [NEO](AtariFileFormats.md) | Yes | Yes | Neochrome |
| PAL | Yes | Yes | Can load raw 768-bytes RGB palettes, as well as JASC Palette. Saving is always performed as JASC Palette |
| other | No | Yes | JPEG, TGA, truecolor PNG can be loaded thanks to the SDL\_image library. This is not always possible on all platforms (ie. on linux if you compile SDL\_image without PNG, you lose the PNG format.) Files that can be loaded this way have no preview in the fileselector. |
If you find a file that grafx2 can't load, please send it to us so we can fix the broken code.
# Other file formats #

These formats aren't yet supported at all, but we are planning to add them in the future
  * OCP Art studio SCR (Amstrad CPC)
  * OCP Art Studio PAL (Amstrad CPC)
  * GraphOS
  * Multiface 2 picture
  * [AtariFileFormats](AtariFileFormats.md)

If you can provide some informations about these formats, please tell us !