# Settings #

## Any click ##

Displays a menu where you can configure some miscellaneous elements of the program:
  * Number of UNDO pages: indicates the total number of pages that GrafX2 will memorize. Each time you modify the picture, its current state is memorized in one of these pages. To flick through these pages, use the "[Oops](Undo.md)" button (Undo/Redo).
  * Font: determines whether you want to use GrafX2 with a classical font, or another one a bit funnier.
  * Mouse sensibility: Modifies the speed of the mouse when you're in fullscreen. With the normal setting (slider on top), you may find the mouse too fast, especially in video modes which are much smaller than your desktop. You can lower the slider to divide the speed by 2, 3 or 4 When using videomodes with native skewed pixels like 640x240 or 320x512, you'll probably want to use a stronger reduction on the axis which has less pixels.
  * Show/Hide in file list: Defines whether some particular files or directories must be displayed by the fileselectors or not.
  * Show/Hide picture limits: Indicates if the picture boundaries must be displayed when you are in a resolution bigger than the picture.
  * Clear palette: Indicates if loading a file with a palette of less than 256 colors must erase the rest of the current palette (replace by the black color).
  * Maximize preview: maximizes the preview of the pictures so that it is as big as possible. If you're not in the same resolution as the picture's one, it can try to correct the aspect ratio, but if the picture does not fill the whole screen, it can be worse.
  * Backup: when you'll save a picture over an existing file, the program will rename this file to "`*`.BAK" where `*` is the name of the picture without its extension. If the backup file already exists in the directory, it will be replaced. If you save a picture with the name of the backup file, no backup file will be created (of course!)
  * Cursor: allows you to choose whether you prefer a solid cursor or a transparent cursor.
  * Safety colors: Brings back the 4 default colors of the menus if you run an operation that passes the image in less than four colors in the palette editor.
  * Adjust brush pick: This option is used when you grab a brush in Grid (Snap) mode. Then, the right-most and down-most pixels won't be picked up with the rest of the brush. This option has been made because, if people grab brushes in Grid mode, that's mostly when they want to grab sprites. For example: if you have 16x16 sprites on your page, you'll set the grid mode to 16x16. But the cursor will snap at points like (0,0), (16,0), (16,16) and so on... And the problem is that, from (0,0) to (16,16), there are 17 pixels! But if you keep the adjust-brush-pick option on, the unwanted pixels will be ignored. Moreover, this option adjusts the brush handle so that the brush still fits in the grid, instead of placing the handle in the center of the brush.
  * Separate colors: Draws a squaring around the colors of the tool-bar.
  * Auto-set resolution: sets the best resolution for the loaded image.
  * Coordinates: Choose if you want to display relative or absolute coordinates when using tools such as circles, rectangles, etc... for example, if you draw a circle: if coords are relative, the radius of the circle will be displayed, while in absolute coords, the coordinates of the cursor will be displayed.
  * Reload: loads the previously saved configuration.
  * Auto-save: means that the configuration will be automatically saved when you'll quit the program.
  * Save: saves the configuration at once.

All modifications will be effective just after closing the menu.