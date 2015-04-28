# The PKM picture format - by Karl Maritaud #

First of all, I'd like to say that I made this file format some years ago when I didn't knew how to load any good format (eg. GIF) and wanted to have my own format.
PKM format was designed to be very simple, easy to encode and decode. Its header is very simple (short) and evolutive.
The only real default I can find in this format is that you can only save 256-color pictures.
I know that you will think:
"Oh no just another fucking format! I'll never use it! Its compression is too poor and I prefer GIF!".
And I'll answer:
"Yeah! You're right. But if you dunno how to load GIF and want a simple format with a quite good compression rate (on simple pictures at least), it could be useful."

So, here comes the format documentation...


# The HEADER: #

The header is the following 780-byte-structure. (Don't worry about the size.
That's just because the palette is considered as a part of the header).

| Pos | Field | Type | Size | Description |
|:----|:------|:-----|:-----|:------------|
| 0 | Signature | char | 3 | Constant string "PKM" (with NO size delimitation '\0' or so...) |
| 3 | Version | byte | 1 | For the moment, it can take only the  value 0. Other packing methods may change this field but there is only one for now... |
| 4 | Pack\_byte | byte | 1 | Value of the recognition byte for color repetitions that are coded on 1 byte. (See the picture packing section for a better explanation) |
| 5 | Pack\_word | byte | 1 | Value of the recognition byte for color repetitions that are coded on 2 bytes. (See the picture packing section...) |
| 6 | Width | word | 2 | Picture width  (in pixels) |
| 8 | Height | word | 2 | Picture height (in pixels) |
| 10 | Palette | byte | 768 | RGB palette (RGB RGB ... 256 times) with values from 0 to 63. I know the standard in picture files is 0 to 255 but I find it stupid! It is really easier to send the whole palette in port 3C9h with a REP OUTSB without palette convertion. |
| 778 | PH\_size | word | 2 | Post-header size. This is the number of bytes between the header and the picture data. This value can be equal to 0. |

# The POST-HEADER: #

> The post-header has a variable size. It was designed to support new features
for this file format without changing the whole format.

> It consists in field identifiers followed by their size and their value.
> A field identifier is coded with 1 byte and a field size also.


## These field identifiers are: ##

(this list may be updated...)

> 0 : Comment on the picture
  1. : Original screen dimensions
> 2 : Back color (transparent color)

> If you encounter a field that you don't know just jump over it. But if a
> field tells you to jump to a position that is over the beginning of the
> picture data, there is an error in the file.


## The fields: ##

  * Comment:

> With this field, artists will be able to comment their pictures.
> Note that GrafX 2 has a comment size limit of 32 chars. But you can
> comment a picture with up to 255 chars if you make your own viewer
> since GrafX 2 will just ignore extra characters.

> Example: [0](0.md),[16](16.md),[by X-Man](Picture.md)
> This sequence means:
> > - the field is a comment
> > - the comment takes 16 characters (there is no end-of-string character
> > > since you know its size)

> > - the comment is "Picture by X-Man"

  * Original screen dimensions:


> Since GrafX 2 supplies a huge range of resolutions, it seemed convenient
> to add a field that indicates what were the original screen dimensions.

> Example: [1](1.md),[4](4.md),[320](320.md),[256](256.md)
> This sequence means:
> > - the field is a screen dimensions descriptor
> > - the dimensions are 2 words (so this value must be always equal to 4)
> > - the original screen width was 320 pixels
> > - the original screen height was 256 pixels


> Note that words stored in fields are written Intel-like. The 90% BETA
> version did not respect this norm. I'm really sorry about this. This is
> not very serious but pictures saved with version 90% and loaded with a
> latest version (91% and more) won't set the right resolution.

  * Back color:

> Saving the back color (transparent color) is especially useful when you
> want to save a brush.
> The size of this field is 1 byte (index of the color between 0 and 255).

> Example: [2](2.md),[1](1.md),[255](255.md)
> This sequence means:
> > - the field is a screen dimensions descriptor
> > - the value takes 1 byte
> > - the transparent color is 255


# The PICTURE PACKING METHOD: #


> The PKM compression method is some sort of Run-Length-Compression which is
very efficient on pictures with long horizontal color repetitions.
> Actually, the compression is efficient if there are often more than 3 times
the same color consecutively.

> I think that it would be better to give you the algorithm instead of swim-
ming in incomprehensible explanations.

```
  BEGIN
    /*
      functions:
        Read_byte(File)       reads and returns 1 byte from File
        Draw_pixel(X,Y,Color) draws a pixel of a certain Color at pos. (X,Y)
        File_length(File)     returns the total length in bytes of File

      variables:
        type of Image_size          is dword
        type of Data_size           is dword
        type of Packed_data_counter is dword
        type of Pixels_counter      is dword
        type of Color               is byte
        type of Byte_read           is byte
        type of Word_read           is word
        type of Counter             is word
        type of File                is <binary file>
    */

    /* At this point you've already read the header and post-header. */

    Image_size          <- Header.Width * Header.Height
    Data_size           <- File_length(File) - (780+Header.PH_size)

    Packed_data_counter <- 0
    Pixels_counter      <- 0

    /* Depacking loop: */
    WHILE ((Pixels_counter<Image_size) AND (Packed_data_counter<Data_size)) DO
    {
      Byte_read <- Read_byte(File)

      /* If it is not a packet recognizer, it's a raw pixel */
      IF ((Byte_read<>Header.Pack_byte) AND (Byte_read<>Header.Pack_word))
      THEN
      {
        Draw_pixel(Pixels_counter MOD Header.Width,
                   Pixels_counter DIV Header.Width,
                   Byte_read)

        Pixels_counter      <- Pixels_counter + 1
        Packed_data_counter <- Packed_data_counter + 1
      }
      ELSE /* Is the number of pixels to repeat coded... */
      {    /* ... with 1 byte */
        IF (Byte_read = Header.Pack_byte) THEN
        {
          Color     <- Read_byte(File)
          Byte_read <- Read_byte(File)

          FOR Counter FROM 0 TO (Byte_read-1) STEP +1
            Draw_pixel((Pixels_counter+Counter) MOD Header.Width,
                       (Pixels_counter+Counter) DIV Header.Width,
                       Color)

          Pixels_counter      <- Pixels_counter + Byte_read
          Packed_data_counter <- Packed_data_counter + 3
        }
        ELSE /* ... with 2 bytes */
        {
          Color     <- Read_byte(File)
          Word_read <- (word value) (Read_byte(File) SHL 8)+Read_byte(File)

          FOR Counter FROM 0 TO (Word_read-1) STEP +1
            Draw_pixel((Pixels_counter+Counter) MOD Header.Width,
                       (Pixels_counter+Counter) DIV Header.Width,
                       Color)

          Pixels_counter      <- Pixels_counter + Word_read
          Packed_data_counter <- Packed_data_counter + 4
        }
      }
    }
  END
```

> For example, the following sequence:
> > (we suppose that Pack\_byte=01 and Pack\_word=02)
> > 04 03 01 05 06 03 02 00 01 2C

> will be decoded as:
> > 04 03 05 05 05 05 05 05 03 00 00 00 ... (repeat 0 300 times (012Ch=300))


> Repetitions that fit in a word must be written with their higher byte first.
> I know that it goes against Intel standard but since I read bytes from the
> file thru a buffer (really faster), I don't care about the order (Sorry :)).
> But words in the header and post-header must be written and read Intel-like!


## Packing advices: ##

  * As you can see, there could be a problem when you'd want to pack a raw
> pixel with a color equal to Pack\_byte or Pack\_word. These pixels should
> always be coded as a packet even if there is only one pixel.

> Example: (we suppose that Pack\_byte=9)
> > 9   will be encoded 9,9,1     (The 1st 9 in the encoded...
> > 9,9 will be encoded 9,9,2     ... sequence is Pack\_byte)
> > etc...

  * It seems obvious to find values for Pack\_byte and Pack\_word that are

> (almost) never used. So a small routine that finds the 2 less used colors
> in the image should be called before starting to pack the picture. This can
> be done almost instantaneously in Assembler.

  * When you want to pack a 2-color-sequence, just write these 2 colors one
> after the other (Color,Color) because it only takes 2 bytes instead of 3 if
> you had to write a packet (Pack\_byte,Color,2).

  * If you pack a very simple picture which has a sequence of more than 65535
> same consecutive bytes, you must break the sequence and continue with a new
> packet.

> Example: you have to pack 65635 same consecutive bytes (eg. color 0)
> > (we suppose that Pack\_byte=01 and Pack\_word=02)
> > You'll write: 02 00 FF FF 01 00 64        (FFFFh=65535, 64h=100)