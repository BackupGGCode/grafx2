# Developer documentation #

  * You can start by reading the [compiling notes](Compiling.md)
  * How we store the sources and data in the [Subversion (svn)](SVNHelp.md) repository.
  * There's some documentation on how to code according to the different [platforms](PlatformDependantCode.md)

## Work in progress and design proposal drafts ##
  * [Pages, layers and animation features](LayersAndAnimation.md)
  * [Enhanced menu system needed for layers and animation](Menubars.md)
  * [EventDrivenInputSystem](EventDrivenInputSystem.md)
  * [INISettingsList](INISettingsList.md)

## File formats ##
  * Grafx2 uses a custom picture format called [PKM](PKMSpec.md). Here are some informations about it.
  * Documentation on [C64 files formats](http://codebase64.org/doku.php?id=base:c64_grafix_files_specs_list_v0.03)
  * Documentation on [Atari file formats](AtariFileFormats.md)

## Program internals ##

  * The source code is documented using Doxygen. The online reference is [here](http://grafx2.googlecode.com/svn/doxydoc/html/index.html). It will help you understand how things work, and if you want to join the project, it will help keep the naming conventions consistent.
  * [Input interface](InputInterface.md) (how Grafx2 handles mouse and keyboard)
  * [Operations engine](OperationsEngine.md) (how to add a new tool)
  * [Loading and saving](LoadSaveSystem.md) (how to add a new file format)