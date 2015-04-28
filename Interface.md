# Grafx2 user interface #

The simplest way to get GrafX2 to run is downloading and running the installer. If you don't want it anymore, go to the add/remove program control panel and uninstall it. Under linux, you will have to build the program from source, sorry. For the other platforms, download the appropriate archive, ectract it and read the README.txt file inside.

Now you can run the program (just double click the grafx2 icon). A window will pop up and display the user interface with a welcome message. It will look like this :

![http://grafx2.googlecode.com/svn/wiki/pictures/startup.png](http://grafx2.googlecode.com/svn/wiki/pictures/startup.png)

As you can see, the screen is divided into various parts. At the bottom, there is a menubar with all the tools you can use. The top part is the drawing area. There you can use your mouse to draw things. Over the drawing area, there is a window. You can notice that it does not look like regular windows from your operating system. This is because Grafx2 uses it's own system for drawing windows. You will have to get used to this way of drawing, as everything inside grafx2 is done like that.

From now on and to avoid confusions, we will use these words :
  * **Screen** is the main window of grafx2, including the menu and the drawing area. All windows are drawn in the screen.
  * **Window** is an internal window of grafx2, like the welcome window. Most of them can be moved inside the screen. The welcome window is not movable and will disapear at the first mouse click.
  * **Menu bar** is the bar at the bottom with all the icons.
  * **Drawing area** is the part of the screen that is not hidden by the menu.
  * **Picture area** is the part of the screen where you can actually draw. It is surrounded by white dashes. It may be bigger or smaller than the drawing area.
  * **status line** is the line of text at the bottom of the menu, displaying some info about what you are doing (usually the mouse coordinates)

Click anywhere on the screen to make the welcome window disapear. Let's start drawing some things.

# Interaction principles #

All the tools share some basic behaviour: left-clicking will draw with the Fore-color while right-clicking will draw with the Back-color.

If a window is opened, Cancel (or No) will always be emulated by the 

&lt;Escape&gt;

 key, and OK (or Yes) by the 

&lt;Return&gt;

 key.

In the different menus, the titles of the buttons that contain an underlined letter can be emulated by pressing this letter on the keyboard.

In some menus, you can select a color range in the palette. This means that you can click on a color and move the mouse to another by maintaining the button pressed to select a color range.

Next page: MenuBar