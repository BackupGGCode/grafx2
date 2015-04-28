# How Grafx2 load and saves files #

Adding a new file format to Grafx2 is quite easy. Let's see how to do it.

The first step is to declare your format. Open **const.h**, this is the file where
all our constants are defined. Increment NB\_KNOWN\_FORMATS, NB\_FORMATS\_LOAD and
NB\_FORMATS\_SAVE. Beware, they are defined twice because we have an optional
dependancy on libpng. In this file you must also add your format to the
**FILE\_FORMATS** enum, in the form FORMAT\_EXT (replacing ext with the extension,
of course). Don't add them after PNG, don't add them before PKM.

The second step is to declare the format so the program makes use of it. This is
done in loadsave.c. Declare your format handler functions. They have no
parameters and return no value. Everything is done with global vars. You should
provide three functions:

  * Test\_EXT tells if you can load the file,
  * Load\_EXT loads a picture,
  * Save\_EXT saves a picture.

You have to register your format in the File\_formats table. The fields are:
  * extension (lowercase, wildcards `*` and ? allowed)
  * Test function
  * Load function
  * Save function
  * Save all picture (should be 1 most of the time, set it to 0 for formats not saving all the data, for example .PAL saves only the palette). You should put a 0 if your format use a lossy compression, like jpeg.
  * Comment allowed. Put an 1 if your format can save a comment in the file. 0 else.

The last step is to code the three functions. Here are the global vars you will
probably need to use.

## Test function ##
Use Get\_full\_filename to get the filename we are asking you to test.
Load your file, do some reading on it to check it is coherent (checking the
header is enough). Set the global var File\_error to 0 if you think you can load
the file, or 1 else.
Don't forget to close your file and free things you allocated (if you did. is
your format so difficult to identify ?)

```
void Test_EXT(void)
{
	FILE* file;
	char filename[MAX_PATH_CHARACTERS];
	long file_size;

	Get_full_filename(filename,0);

	file = fopen(filename,"rb");

	if(file)
	{
		// Do some more tests to see if everything is ok
		if((/*...*/)
			File_error = 0;
		else
			File_error = 1;
		fclose(file)
	}
	else
		File_error = 1;
}
```

## Load function ##
This one is a bit more tricky. You have to handle some things for our preview
window. You can still set File\_error while loading the file if something goes wrong, that's why you don't have to go too far in the Test function. Get the filename the same way with Get\_full\_filename, read the data.
You have to set some variables and call some functions, of course.

```
void Test_EXT(void)
{
	FILE* file;
	char filename[MAX_PATH_CHARACTERS];
	long file_size;

	Get_full_filename(filename,0);

	file = fopen(filename,"rb");

	if(file)
	{
		int file_size = File_length_file(file);
		T_Palette pal;
		word width, height;
		word x, y;
		byte* buffer

		// read the header

		Init_preview(width, height, filesize, FORMAT_EXT); // Do this as soon as you can

		Main_image_width = width ;
		Main_image_height = height;

		buffer = malloc(width);

		// Read one line at a time to avoid useless i/o.
		// But you can do otherwise if your format isn't friendly enough.
		for(y=0; y<height; y++)
		{
			Read_bytes(file,buffer,width);
			for(x=0; x<width; x++)
				Pixel_load_function(x,y,buffer[x]);
		}

		free(buffer);

		memcpy(Main_palette,pal); // this set the software palette for grafx2
		Set_palette(Main_palette); // this set the hardware palette for SDL
		Remap_fileselector(); // Always call it if you change the palette
		
		File_error = 0;
		fclose(file);
	}
	else
		File_error = 1;
}
```

So, to sum up :
  * Set Main\_image\_width and Main\_image\_height to the appropriate value (the maximum image size is 10 000x10 000 pixels),
  * Call Init\_preview(width, height, filesize, FORMAT\_EXT),
  * Load your palette as {byte R, byte G, byte B}[256](256.md) in Main\_palette then call Set\_palette(Main\_palette),
  * Load the image data calling Pixel\_load\_function(x,y,color) for each pixel, in any order you want.

## Save function ##
It's simpler than the load, as you don't have to handle a preview.
As usual, get the filename, open the file, write everything, then close the file. Set File\_error if something went bad (permission denied on fopen for example). Don't forget to close file and free any buffer.

## Helper function and endianness ##
As you've seen in the examples, we dont use fread and fwrite directly. There is a good reason: these functions don't care about endianness.
We provide functions that do it properly. They all return 1 if everything went fine and 0 if they fail.

```
int Read_bytes(FILE *file, void *dest, size_t size);
int Write_bytes(FILE *file, void *dest, size_t size);

int Read_byte(FILE *file, byte *dest);
int Write_byte(FILE *file, byte b);

int Read_word_le(FILE *file, word *dest);
int Write_word_le(FILE *file, word w);
int Read_dword_le(FILE *file, dword *dest);
int Write_dword_le(FILE *file, dword dw);

int Read_word_be(FILE *file, word *dest);
int Write_word_be(FILE *file, word w);
int Read_dword_be(FILE *file, dword *dest);
int Write_dword_be(FILE *file, dword dw);
```

Read\_bytes read a number of bytes without any endianness processing. Use that to process the main pixel data of your image if applicable, to avoid many io requests to the OS.

Read\_byte reads one single byte. No endianness problem.

The `*_`le functions read and write little-endian as used on x86, while `*_`be read and write big endian as on 68000. Check your format info to see what you need to use. Note some functions in our current loadsave.c loads and save a lot of things (for example a whole header with read/write\_bytes() and then parse it. Please don't do that. It's not clean, it's error prone, and you will encounter struct-packing headaches. Dont use `__`attribute(`__`packed`__`), the linux/sparc version will crash if you do.