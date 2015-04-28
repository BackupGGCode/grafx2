# Grafx2 2.2 release notes #

Grafx2 2.2 (since [revision 1375](https://code.google.com/p/grafx2/source/detail?r=1375) - 4 March 2010) has changed the way its directory is organized. The **executable is now in a sub-directory called "bin"**, and all the run-time data are is moved to a subdirectory "share/grafx2". This means that if you install it over a previous installation, many old files will not be overwritten. This can lead to some confusion, especially if you run the old executable.

Because of this, if you're upgrading an old version (2.0 / 2.1 / 2.2wip) to 2.2 in the same directory, you should start by **uninstalling** the previous installation :
  * Either by using the Program manager (if you had used the installer),
  * or by deleting the files manually.

Alternatively, you can choose to install in a new directory, outside of the .

In any case, note that any shortcut to Grafx2 should now point to _(install\_directory)_\**bin**\grafx2.exe