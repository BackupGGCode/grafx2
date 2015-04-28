This is a copy of the document "ST Picture Formats" : [picfmts.doc](http://www.umich.edu/~archive/atari/Graphics/picfmts.doc)

We use it as a reference for implementing NEOchrome images support.

The original document is enclosed in tags to prevent wiki formatting, but otherwise unmodified.


---

<pre>
<pre><code>                           ST Picture Formats<br>
                           ------------------<br>
                               Edited by:<br>
<br>
                              David Baggett<br>
                         5640 Vantage Point Road<br>
                         Columbia, MD  21044 USA<br>
                             (301)  596-4779    <br>
                          (usenet: dmb@TIS.COM)<br>
<br>
                   (Please report errors or additions.)<br>
<br>
        Copyright (C) 1988, 1989, 1990, 1991 by David M. Baggett<br>
<br>
<br>
    Non-profit redistribution of this document is permitted, provided<br>
    the document is not modified in any way.<br>
<br>
    Reproduction of this document in whole or in part for  commercial<br>
    purposes is expressly forbidden without the prior written consent<br>
    of David M. Baggett.<br>
<br>
    The  information  presented here is not guaranteed to be correct.<br>
    The editor and contributors will in no event be liable for direct,<br>
    indirect, incidental, or consequential damages resulting from the <br>
    use of the information in this document.<br>
<br>
    This document is the product of many hours of volunteer work by a<br>
    large number of people. Please respect this -- do not violate the<br>
    distribution policy.<br>
<br>
<br>
                              CONTRIBUTORS<br>
  <br>
    Steve Belczyk  Phil Blanchfield  Jason Blochowiak  John Brochu**<br>
       David Brooks  Daniel Deimert  Neil Forsyth   Stefan Hoehn  <br>
        Gerfried Klein   Ken MacLeod  Jim McCabe  Darek Mihocka   <br>
         David Mumper   George Nassas   George Seto  Joe Smith  <br>
              Greg Wageman   Roland Waldi*  Gerry Wheeler<br>
<br>
<br>
                                Contents <br>
                                --------<br>
<br>
        NEOchrome                               *.NEO<br>
        NEOchrome Animation                     *.ANI<br>
        DEGAS                                   *.PI?   ? = 1, 2, 3<br>
        DEGAS Elite                             *.PI?   ? = 1, 2, 3<br>
        DEGAS Elite (Compressed)                *.PC?   ? = 1, 2, 3<br>
        Tiny                                    *.TN?   ? = 1, 2, 3, Y<br>
        Spectrum 512                            *.SPU<br>
        Spectrum 512 (Compressed)               *.SPC<br>
        Art Director                            *.ART<br>
        C.O.L.R. Object Editor Mural            *.MUR<br>
        Doodle                                  *.DOO<br>
        Animatic Film                           *.FLM<br>
        GEM Bit Image                           *.IMG<br>
        STAD                                    *.PAC<br>
        Imagic Film/Picture                     *.IC?   ? = 1, 2, 3<br>
        IFF                                     *.IFF<br>
        MacPaint                                *.MAC<br>
        PackBits Compression Algorithm<br>
 <br>
<br>
                        Introductory Information<br>
                        ------------------------<br>
word    = 2 bytes<br>
long    = 4 bytes<br>
palette = Hardware color palette, stored as 16 words.  First word is<br>
          color register zero (background), last word is color register<br>
          15.  Each word has the form:<br>
<br>
          Bit:  (MSB) 15 14 13 12 11 10 09 08 07 06 05 04 03 02 01 00 (LSB)<br>
                      -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --<br>
                       0  0  0  0  0 R2 R1 R0  0 G2 G1 G0  0 B2 B1 B0<br>
<br>
          R2 = MSB of red intensity<br>
          R0 = LSB of red intensity<br>
<br>
          G2 = MSB of green intensity<br>
          G0 = LSB of green intensity<br>
<br>
          B2 = MSB of blue intensity<br>
          B0 = LSB of blue intensity<br>
<br>
          Intensity ranges from 0 (color not present) to 7 (highest<br>
          intensity).<br>
<br>
          Example: { red = 7, green = 3, blue = 5 } -&gt; 0735 (hex)<br>
<br>
          Caveat:  It is wise to mask off the upper four bits of each<br>
                   palette entry, since a few programs store special<br>
                   information there (most notably Art Studio).<br>
<br>
<br>
                             The Formats<br>
                             -----------<br>
<br>
&lt;NEOchrome&gt;     *.NEO<br>
 <br>
1 word          flag byte [always 0]<br>
1 word          resolution [0 = low res, 1 = medium res, 2 = high res]<br>
16 words        palette<br>
12 bytes        filename [usually "        .   "]<br>
1 word          color animation limits.  High bit (bit 15) set if color<br>
                animation data is valid.  Low byte contains color animation<br>
                limits (4 most significant bits are left/lower limit,<br>
                4 least significant bits are right/upper limit).<br>
1 word          color animation speed and direction.  High bit (bit 15) set<br>
                if animation is on.  Low order byte is # vblanks per step.<br>
                If negative, scroll is left (decreasing).  Number of vblanks<br>
                between cycles is |x| - 1<br>
1 word          # of color steps (as defined in previous word) to display<br>
                picture before going to the next.  (For use in slide shows)<br>
1 word          image X offset [unused, always 0]<br>
1 word          image Y offset [unused, always 0]<br>
1 word          image width [unused, always 320]<br>
1 word          image height [unused, always 200]<br>
33 words        reserved for future expansion<br>
16000 words     picture data (screen memory)<br>
-----------<br>
32128 bytes     total<br>
 <br>
<br>
&lt;NEOchrome Animation&gt;        *.ANI<br>
<br>
NOTE:      To get this feature on versions 0.9 and later select the Grabber<br>
        icon and click both mouse buttons in the eye of the second R in the<br>
        word GRABBER.<br>
           Interestingly enough, some versions of NEO only require you<br>
        to press the right button, not both.  Hmmm...<br>
<br>
1 long          magic number BABEEBEA (hex) (seems to be ignored)<br>
1 word          width of image in bytes (always divisible by 8)<br>
1 word          height of image in scan lines<br>
1 word          size of image in bytes + 10 (!)<br>
1 word          x coordinate of image (must be divisible by 16) - 1<br>
1 word          y coordinate of image - 1<br>
1 word          number of frames<br>
1 word          animation speed (# vblanks to delay between frames)<br>
1 long          reserved; should be zero<br>
--------<br>
22 bytes        total for header<br>
<br>
? words         image data (words of screen memory) for each frame, in <br>
                order<br>
<br>
<br>
&lt;DEGAS&gt;         *.PI1 (low resolution)<br>
                *.PI2 (medium resolution)<br>
                *.PI3 (high resolution)<br>
<br>
1 word          resolution (0 = low res, 1 = medium res, 2 = high res)<br>
                Other bits may be used in the future; use a simple bit<br>
                test rather than checking for specific word values.<br>
16 words        palette<br>
16000 words     picture data (screen memory)<br>
-----------<br>
32034 bytes     total<br>
<br>
<br>
&lt;DEGAS Elite&gt;   *.PI1 (low resolution)<br>
                *.PI2 (medium resolution)<br>
                *.PI3 (high resolution)<br>
<br>
1 word          resolution (0 = low res, 1 = medium res, 2 = high res)<br>
                Other bits may be used in the future; use a simple bit<br>
                test rather than checking for specific word values.<br>
16 words        palette<br>
16000 words     picture data (screen memory)<br>
4 words         left color animtion limit table (starting color numbers)<br>
4 words         right color animation limit table (ending color numbers)<br>
4 words         animation channel direction flag (0 = left, 1 = off, 2 = right)<br>
4 words         128 - animation channel delay in 1/60's of a second. [0 - 128]<br>
                (I.e., subtract word from 128 to get 1/60th's of a second.)<br>
-----------<br>
32066 bytes     total<br>
<br>
<br>
&lt;DEGAS Elite (Compressed)&gt;      *.PC1 (low resolution)<br>
                                *.PC2 (medium resolution)<br>
                                *.PC3 (high resolution)<br>
 <br>
1 word          resolution (same as Degas, but high order bit is set;<br>
                i.e., hex 8000 = low res, hex 8001 = medium res,<br>
                hex 8002 = high res).  Other bits may be used in the<br>
                future; use a simple bit test rather than checking<br>
                for specific word values.<br>
16 words        palette<br>
&lt; 32000 bytes   control/data bytes<br>
4 words         left color animation limit table (starting color numbers)<br>
4 words         right color animation limit table (ending color numbers)<br>
4 words         animation channel direction flag [0 = left, 1 = off, 2 = right]<br>
4 words         128 - animation channel delay in 1/60's of a second. [0 - 128]<br>
                (I.e., subtract word from 128 to get 1/60th's of a second.)<br>
-----------<br>
&lt; 32066 bytes   total<br>
 <br>
Compression Scheme:<br>
 <br>
   PackBits compression is used (see below).  Each scan line is compressed<br>
separately; i.e., all data for a given scan line appears before any data<br>
for the next scan line.  The scan lines are specified from top to bottom<br>
(i.e., 0 is first).  For each scan line, all the data for a given bit plane<br>
appears before any data for the next higher order bit plane.  Note this is<br>
identical to the IFF 'BODY' image data.<br>
   To clarify:  The first data in the file will be the data for the lowest<br>
order bit plane of scan line zero, followed by the data for the next higher<br>
order bit plane of scan line zero, etc., until all bit planes have been<br>
specified for scan line zero.  The next data in the file will be the data<br>
for the lowest order bit plane of scan line one, followed by the data for<br>
the next higher order bit plane of scan line one, etc., until all bit planes<br>
have been specified for all scan lines.<br>
 <br>
Caveats:<br>
 <br>
   DEGAS Elite's picture loading routine places some restrictions on<br>
compressed DEGAS files:<br>
 <br>
        o Elite uses a 40-byte buffer to store data being decompressed.<br>
 <br>
        o Whenever a control command is encountered, bytes are stuffed<br>
        in this buffer.<br>
 <br>
        o The buffer is only emptied when there are EXACTLY 40<br>
        characters in it.<br>
 <br>
The important conclusion here is that<br>
 <br>
        No control command may cause the buffer to have more than 40<br>
        bytes in it.  In other words, all control commands must end on<br>
        or before the 40-byte boundary.<br>
 <br>
Any picture violating the last condition will cause Elite to get a bus<br>
error when the picture is loaded.<br>
 <br>
<br>
&lt;Tiny&gt;  *.TNY (any resolution)<br>
        *.TN1 (low resolution)<br>
        *.TN2 (medium resolution)<br>
        *.TN3 (high resolution)<br>
<br>
   Several people have reported sightings of mutated Tiny pictures that<br>
do not follow the standard format, so let's be careful out there.  What<br>
is described here is the format that David Mumper's original<br>
TNYSTUFF.PRG produces.<br>
<br>
1 byte          resolution (same as NEO, but +3 indicates rotation<br>
                information also follows)<br>
<br>
If resolution &gt; 2 {<br>
1 byte          left and right color animation limits.  High 4 bits<br>
                hold left (start) limit; low 4 bits hold right (end)<br>
                limit<br>
1 byte          direction and speed of color animation (negative value<br>
                indicates left, positive indicates right, absolute value<br>
                is delay in 1/60's of a second.<br>
1 word          color rotation duration (number of iterations)<br>
}<br>
<br>
16 words        palette<br>
1 word          number of control bytes<br>
1 word          number of data words<br>
3-10667 bytes   control bytes<br>
1-16000 words   data words<br>
-------------<br>
42-32044 bytes  total<br>
<br>
Control byte meanings:<br>
<br>
        For a given control byte, x:<br>
<br>
        x &lt; 0   Absolute value specifies the number of unique words to<br>
                take from the data section (from 1 to 127)<br>
        x = 0   1 word is taken from the control section which specifies<br>
                the number of times to repeat the next data word (from<br>
                128 to 32767)<br>
        x = 1   1 word is taken from the control section which specifies<br>
                the number of unique words to be taken from the data<br>
                section (from 128 - 32767)<br>
        x &gt; 1   Specifies the number of times to repeat the next word<br>
                taken from the data section (from 2 to 127)<br>
<br>
Format of expanded data:<br>
<br>
   The expanded data is not simply screen memory bitmap data; instead, the <br>
data is divided into four sets of vertical columns.  (This results in<br>
better compression.)  A column consists of one specific word taken<br>
from each scan line, going from top to bottom.  For example, column 1 <br>
consists of word 1 on scanline 1 followed by word 1 on scanline 2, etc., <br>
followed by word 1 on scanline 200.<br>
   The columns appear in the following order:<br>
<br>
   1st set contains columns 1, 5,  9, 13, ..., 69, 73, 77 in order<br>
   2nd set contains columns 2, 6, 10, 14, ..., 70, 74, 78 in order<br>
   3rd set contains columns 3, 7, 11, 15, ..., 71, 75, 79 in order<br>
   4th set contains columns 4, 8, 12, 16, ..., 72, 76, 80 in order<br>
<br>
Note that Tiny partitions the screen this way regardless of resolution; i.e., <br>
these aren't bitplanes.  For example, medium resoltion only has two bitplanes, <br>
but Tiny still divides medium resolution pictures into four parts.<br>
<br>
<br>
&lt;Spectrum 512&gt;  *.SPU<br>
<br>
80 words        first scan line of picture (unused) -- should be zeroes<br>
15920 words     picture data (screen memory) for scan lines 1 through 199<br>
9552 words      3 palettes for each scan line (the top scan line is<br>
                not included because Spectrum 512 can't display it)<br>
-----------<br>
51104 bytes     total<br>
<br>
Note that the Spectrum 512 mode's three palette changes per scan<br>
line allow more colors on the screen than normally possible, but a<br>
tremendous amount of CPU time is required to maintain the image.<br>
<br>
The Spectrum format specifies a palette of 48 colors for each scan line.<br>
To decode a Spectrum picture, one must be know which of these 48 colors<br>
are in effect for a given horizontal pixel position.<br>
<br>
Given an x-coordinate (from 0 to 319) and a color index (from 0 to 15),<br>
the following C function will return the proper index into the Spectrum<br>
palette (from 0 to 47):<br>
<br>
/*<br>
 *  Given an x-coordinate and a color index, returns the corresponding<br>
 *  Spectrum palette index.<br>
 *<br>
 *  by Steve Belczyk; placed in the public domain December, 1990.<br>
 */<br>
int <br>
FindIndex(x, c)<br>
	int x, c;<br>
{<br>
	int x1;<br>
<br>
	x1 = 10 * c;<br>
<br>
	if (1 &amp; c)		/* If c is odd */<br>
		x1 = x1 - 5;<br>
	else			/* If c is even */<br>
		x1 = x1 + 1;<br>
<br>
	if (x &gt;= x1 &amp;&amp; x &lt; x1 + 160) <br>
		c = c + 16;<br>
	else if (x &gt;= x1 + 160) <br>
		c = c + 32;<br>
<br>
	return c;<br>
}<br>
<br>
<br>
&lt;Spectrum 512 (Compressed)&gt;        *.SPC<br>
 <br>
1 word          flag word [$5350 or "SP"]<br>
1 word          reserved for future use [always 0]<br>
1 long          length of data bit map<br>
1 long          length of color bit map<br>
&lt;= 32092 bytes  compressed data bit map<br>
&lt;= 17910 bytes  compressed color bit map<br>
--------------<br>
&lt;= 50014 bytes   total<br>
 <br>
Data compression:<br>
 <br>
   Compression is via a modified run length encoding (RLE) scheme,<br>
similar to DEGAS compressed and Tiny.  The data map is stored as a<br>
sequence of records.  Each record consists of a header byte followed by<br>
one or more data bytes.  The meaning of the header byte is as follows:<br>
 <br>
        For a given header byte, x:<br>
 <br>
           0 &lt;= x &lt;= 127   Use the next x + 1 bytes literally (no repetition)<br>
        -128 &lt;= x &lt;=  -1   Use the next byte -x + 2 times<br>
 <br>
The data appears in the following order:<br>
 <br>
        1. Picture data, bit plane 0, scan lines 1 - 199<br>
        2. Picture data, bit plane 1, scan lines 1 - 199<br>
        3. Picture data, bit plane 2, scan lines 1 - 199<br>
        4. Picture data, bit plane 3, scan lines 1 - 199<br>
 <br>
Decompression of data ends when 31840 data bytes have been used.<br>
 <br>
Color map compression:<br>
 <br>
   Each 16-word palette is compressed separately.  There are three<br>
palettes for each scan line (597 total).  The color map is stored as a<br>
sequence of records.  Each record starts with a 1-word bit vector which<br>
specifies which of the 16 palette entries are included in the data<br>
following the bit vector (1 = included, 0 = not included).  If a palette<br>
entry is not included, it is assumed to be zero (black).  The least<br>
significant bit of the bit vector refers to palette entry zero, while the<br>
most significant bit refers to palette entry 15.  Bit 15 must be zero,<br>
since Spectrum 512 does not use palette entry 15.  Bit 0 should also be<br>
zero, since Spectrum 512 always makes the background color black.<br>
   The words specifying the values for the palette entries indicated in<br>
the bit vector follow the bit vector itself, in order (0 - 15).<br>
<br>
<br>
&lt;Art Director&gt;  *.ART (low resolution only)<br>
<br>
16000 words     picture data (screen memory)<br>
16 words        palette<br>
15 * 16 words   15 more palettes for animation<br>
-------------<br>
32512 bytes     total<br>
<br>
<br>
&lt;C.O.L.R. Object Editor Mural&gt;        *.MUR (low resolution only)<br>
<br>
16000 words     picture data (screen memory)<br>
                (palettes are stored in separate files)<br>
-----------<br>
32000 bytes     total<br>
<br>
<br>
&lt;Doodle&gt;        *.DOO (high resolution only)<br>
<br>
16000 words     picture data (screen memory)<br>
-----------<br>
32000 bytes     total<br>
<br>
<br>
&lt;Animatic Film&gt; *.FLM (low resolution only)<br>
<br>
1 word          number of frames<br>
16 words        palette<br>
1 word          speed (0 - 99; value is 99 - # vblanks to delay between frames)<br>
1 word          direction (0 = forwards, 1 = backwards)<br>
1 word          end action (what to do after the last frame)<br>
                0 = pause, then repeat from beginning<br>
                1 = immediately repeat from beginning<br>
                2 = reverse (change direction)<br>
1 word          width of film in pixels<br>
1 word          height of film in pixels<br>
1 word          Animatic version number (major)<br>
1 word          Animatic version number (minor)<br>
1 long          magic number 27182818 (hex)<br>
3 longs         reserved for expansion (should be all zeros)<br>
--------<br>
32 words        total for header<br>
<br>
? words         image data (words of screen memory) for each frame, in order<br>
<br>
<br>
&lt;GEM Bit Image&gt; *.IMG<br>
 <br>
1 word          version number of image file [1]<br>
1 word          length of header in words [usually 8]<br>
1 word          number of color planes [1 for monochrome]<br>
1 word          pattern length in bytes [1-8, usually 2 for screen images]<br>
1 word          pixel width in microns (1/1000 mm, 25400 microns per inch)<br>
1 word          pixel height in microns<br>
1 word          line width in pixels<br>
1 word          number of lines<br>
-------<br>
? words         header length defined in 2nd word of header<br>
 <br>
? bytes         data<br>
 <br>
NOTES:  If the image is a color image (planes &gt; 1), the planes are stored<br>
separately starting with plane 0.  There is, however, no standard way of<br>
storing the color palette.  Some programs may save the palette in separate<br>
files, some may extend the header.  For this reason, you should never<br>
assume the header is 8 words long, always get the header length from the<br>
2nd word of the header.  Also, the line width in the 7th word is the number<br>
of pixels in a line.  Since the data is encoded in byte-wide packets, the<br>
actual unpacked line width is always a multiple of 8, and may be 1-7 pixels<br>
longer than the length specified in the header.<br>
<br>
For each byte x in the data section,<br>
 <br>
        x = 0           Pattern/scanline run.<br>
                        Read the next byte, n (unsigned).<br>
 <br>
                        If n &gt; 0 then:<br>
                                Read a number of bytes equal to the "pattern<br>
                                length" word in the header.  Repeat this<br>
                                pattern n times.<br>
 <br>
                        If n = 0 then:<br>
                                Scanline run.  Data for the next scanline<br>
                                is to be used multiple times.  Read the<br>
                                following record:<br>
 <br>
                                1 byte          flag byte [$FF]<br>
                                1 byte          number of times to use<br>
                                                next scanline data<br>
 <br>
                                The data for the next scanline follows,<br>
                                compressed normally.<br>
 <br>
        x = 80 (hex)    Uncompressed bit string.  The next byte<br>
                        determines the number of bytes to use<br>
                        literally.  The literal data bytes follow.<br>
 <br>
        otherwise       Solid run.  The value of x determines<br>
                        what to draw.  The high bit specifies whether<br>
                        the pixels are set or cleared.  A 1 indicates<br>
                        a byte-run using $FF, a 0 indicates a byte-run<br>
                        using $00.  The low 7 bits, taken as an unsigned<br>
                        quantity, specify the length of the run in bytes.<br>
 <br>
<br>
&lt;STAD&gt;          *.PAC (high resolution only)<br>
<br>
4 bytes         "pM86" (vertically packed) or "pM85" (horizontally packed)<br>
1 byte          id byte<br>
1 byte          pack byte (most frequently occuring byte in bitmap)<br>
1 byte          "special" byte<br>
-------<br>
7 bytes         total for header<br>
<br>
? bytes         data<br>
<br>
The data is encoded as follows.  For each byte x in the data section:<br>
<br>
        x = id byte             Read one more byte, n.  Use pack byte <br>
                                n + 1 times.<br>
        x = "special" byte      Read two more bytes, d, and n (in order).<br>
                                Use byte d n times.<br>
        otherwise               Use byte x literally.<br>
<br>
<br>
&lt;Imagic Film/Picture&gt;           *.IC1 (low resolution)<br>
                                *.IC2 (medium resolution)<br>
                                *.IC3 (high resolution)<br>
<br>
4 bytes         "IMDC"<br>
1 word          resolution (0 = low res, 1 = medium res, 2 = high res)<br>
16 words        palette<br>
1 word          date (GEMDOS format)<br>
1 word          time (GEMDOS format)<br>
8 bytes         name of base picture file (for delta compression), or zeroes<br>
1 word          length of data (?)<br>
1 long          registration number<br>
8 bytes         reserved<br>
1 byte          compressed? (0 = no, 1 = yes)<br>
<br>
If compressed {<br>
1 byte          delta-compressed? (-1 = no, &gt; -1 = yes)<br>
1 byte          ?<br>
1 byte          escape byte<br>
}<br>
-------<br>
65 bytes        total for header (68 bytes if compressed)<br>
<br>
? bytes         data<br>
<br>
   Compressed data may be either stand-alone or delta-compressed (relative<br>
to the base picture named in the header).  Delta compression involves<br>
storing only how the picture differs from the base picture (i.e., only<br>
portions of the screen that have changed are stored).  This is used to<br>
to encode animated sequences efficiently.<br>
<br>
Compressed data, stand-alone:<br>
<br>
For each byte x in the data section:<br>
<br>
        x = escape byte         Read one more byte, n.  (n is unsigned).<br>
<br>
                                If n &gt;= 2, use the next byte n times.<br>
                                If n = 1, keep reading bytes until a<br>
                                byte k not equal to 1 is encountered.<br>
                                Then read the next byte d.<br>
                                If the number of 1 bytes encountered is o,<br>
                                use d (256 * o + k) times.  I.e.,<br>
<br>
                                if (n == 1) {<br>
                                        o = 0;<br>
                                        while (n == 1) {<br>
                                                o++;<br>
                                                n = next byte;<br>
                                        }<br>
<br>
                                        k = n;<br>
                                        d = next byte;<br>
<br>
                                        Use d (256 * o + k) times.<br>
                                }<br>
                                else {<br>
                                        d = next byte;<br>
                                        Use d (n) times.<br>
                                }<br>
<br>
        x != escape byte        Use x literally.<br>
<br>
Compressed data, delta compressed:<br>
<br>
For each byte x in the data section:<br>
<br>
        x = escape byte         Read one more byte, n.  (n is unsigned).<br>
<br>
                                If n &gt;= 3, use the next byte n times.<br>
                                If n = 1, do the same as for n = 1 in<br>
                                stand-alone compression (above).<br>
                                If n = 2, then set n = next byte.<br>
                                        If n = 0, end of picture.<br>
                                        If n &gt;= 2, take n bytes from base<br>
                                        picture.<br>
                                        If n = 1, do the same as for n = 1<br>
                                        in stand-alone compression (above),<br>
                                        but take (256 * o + k) bytes from <br>
                                        base picture.<br>
<br>
        x != escape byte        Use x literally.<br>
<br>
<br>
&lt;IFF Format&gt;    *.IFF<br>
 <br>
4 bytes         "FORM" (FORM chunk ID)<br>
1 long          length of file that follows<br>
4 bytes         "ILBM" (InterLeaved BitMap file ID)<br>
<br>
4 bytes         "BMHD" (BitMap HeaDer chunk ID)<br>
1 long          length of chunk [20]<br>
20 bytes        1 word = image width in pixels<br>
                1 word = image height in lines<br>
                1 word = image x-offset [usually 0]<br>
                1 word = image y-offset [usually 0]<br>
                1 byte = # bitplanes<br>
                1 byte = mask (0=no, 1=impl., 2=transparent, 3=lasso)<br>
                1 byte = compressed [1] or uncompressed [0]<br>
                1 byte = unused [0]<br>
                1 word = transparent color (for mask=2)<br>
                1 byte = x-aspect [5=640x200, 10=320x200/640x400, 20=320x400]<br>
                1 byte = y-aspect [11]<br>
                1 word = page width (usually the same as image width)<br>
                1 word = page height (usually the same as image height)<br>
<br>
4 bytes         "CMAP" (ColorMAP chunk ID)<br>
1 long          length of chunk [3*n where n is the # colors]<br>
3n bytes        3 bytes per RGB color.  Each color value is a byte<br>
                and the actual color value is left-justified in the<br>
                byte such that the most significant bit of the value<br>
                is the MSB of the byte.  (ie. a color value of 15 ($0F)<br>
                is stored as $F0)  The bytes are stored in R,G,B order.<br>
<br>
4 bytes         "CRNG" (Color RaNGe chunk ID)<br>
1 long          length of chunk [8]<br>
8 bytes         1 word = reserved [0]<br>
                1 word = animation speed (16384 = 60 steps per second)<br>
                1 word = active [1] or inactive [0]<br>
                1 byte = left/lower color animation limit<br>
                1 byte = right/upper color animation limit<br>
<br>
4 bytes         "CAMG" (Commodore AMiGa viewport mode chunk ID)<br>
1 long          length of chunk [4]<br>
1 long          viewport mode bits (bit 11 = HAM, bit 3 = interlaced)<br>
<br>
4 bytes         "BODY" (BODY chunk ID)<br>
1 long          length of chunk [# bytes of image data that follow]<br>
? bytes         actual image data<br>
 <br>
NOTES: Some of these chunks may not be present in every IFF file, and may<br>
not be in this order.  You should always look for the ID bytes to find a<br>
certain chunk.  All chunk IDs are followed by a long value that tells the<br>
size of the chunk.  This is the number of bytes that FOLLOW the 4 ID bytes<br>
and size longword.  The exception to this is the FORM chunk.  The size<br>
longword that follows the FORM ID is the size of the remainder of the file.<br>
The FORM chunk must always be the first chunk in an IFF file.<br>
<br>
The R,G,B ranges of AMIGA and ST are different (AMIGA 0...15, ST 0...7),<br>
as is the maximum number of bitplanes (AMIGA: 5, ST: 4).<br>
<br>
Format of body data<br>
 <br>
An expanded picture is simply a bitmap.  The packing method is PackBits<br>
(see below), and is identical to MacPaint and DEGAS Elite compressed.<br>
 <br>
The (decompressed) body data appears in the following order:<br>
 <br>
        line 1 plane 0 ... line 1 plane 1 ... ... line 1 plane m<br>
        [line 1 mask (if appropriate)]<br>
        line 2 plane 0 ... line 2 plane 1 ... ... line 2 plane m<br>
        [line 2 mask (if appropriate)]<br>
        ...<br>
        line x plane 0 ... line x plane 1 ... ... line x plane m<br>
        [line x mask (if appropriate)]<br>
 <br>
The FORM chunk identifies the type of data:<br>
 <br>
        "ILBM" = interleaved bit map<br>
        "8SVX" = 8-bit sample voice<br>
        "SMUS" = simple music score<br>
        "FTXT" = formatted text (Amiga)<br>
 <br>
<br>
&lt;MacPaint&gt;      *.MAC<br>
 <br>
1 long          version number [0=ignore header, 2=header valid]<br>
38 * 8 bytes    8x8 brush/fill patterns.  Each byte is a pattern row,<br>
                and the bytes map the pattern rows top to bottom.  The<br>
                patterns are stored in the order they appear at the bottom<br>
                of the MacPaint screen top to bottom, left to right.<br>
204 bytes       unused<br>
-------------<br>
512 bytes       total for header<br>
<br>
&lt; 51200 bytes   compressed bitmap data<br>
-------------<br>
&lt; 51712 bytes   total<br>
 <br>
NOTE:  The version number is actually a flag to MacPaint to indicate if<br>
the brush/fill patterns are present in the file.  If the version is 0,<br>
the default patterns are used.  Therefore you can simply save a MacPaint<br>
file by writing a blank header (512 $00 bytes), followed by the packed<br>
image data.<br>
<br>
Bitmap compression:<br>
 <br>
   The bitmap data is for a 576 pixel by 720 pixel monochrome image.<br>
The packing method is PackBits (see below).  There are 72 bytes per<br>
scan line.  Each bit represents one pixel; 0 = white, 1 = black.<br>
 <br>
<br>
&lt;PackBits Compression Algorithm&gt;<br>
<br>
The following packing algorithm originated on the Mac, was adopted by<br>
Electronic Arts/Commodore for use in the IFF standard, and then by Tom<br>
Hudson for use in DEGAS Elite.  The algorithm is currently used in<br>
MacPaint, IFF, and DEGAS Elite compressed file formats.  Each scan line<br>
is packed separately, and packing never extends beyond a scan line.<br>
<br>
For a given control byte 'n':<br>
    0 &lt;= n &lt;= 127   : use the next n + 1 bytes literally (no repetition).<br>
 -127 &lt;= n &lt;= -1    : use the next byte -n + 1 times.<br>
         n = -128   : no operation, not used.<br>
<br>
-------------------------------------------------------------------------<br>
<br>
* Roland Waldi contributed extensive information on the following formats:<br>
<br>
        GEM, IMG, Doodle, STAD, Imagic Film/Picture, Art Director, IFF<br>
<br>
** John Brochu, ST picture formats guru, provided sage advice and many<br>
   corrections to the following formats:<br>
<br>
        NeoChrome, DEGAS Elite Compressed, Spectrum 512 Compressed,<br>
        GEM Bit Image, IFF, MacPaint<br>
<br>
Version of Wed Dec 19 11:20:55 EST 1990<br>
Cosmetic changes Tue Jan 29 00:17:51 EST 1991<br>
</code></pre>
</pre>

---

End of picfmts.doc