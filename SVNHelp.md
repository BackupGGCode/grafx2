# Subversion repository #
The source code of grafx2 is stored in a Subversion (aka SVN) repository, where all versions of each file are available. The web site http://code.google.com/p/grafx2/ allows browsing through it (read-only), but developers can use a Subversion client for full access.
We often use the svn revision number to identify a particular set of change.

# Location #

To quote googlecode's [checkout](http://code.google.com/p/grafx2/source/checkout) page:

Project members authenticate over HTTPS to allow committing changes.

```
svn checkout https://grafx2.googlecode.com/svn/trunk/ grafx2 --username yrizoud
```

When prompted, enter your [generated googlecode.com password](http://code.google.com/hosting/settings).

_note: This creates a new working space in (new?) directory **grafx2**_



---


## Repository tree ##
### trunk ###
This is where most work takes place. It contains at all times the work-in-progress version, sometimes unstable. When publishing a stable version, the code in trunk is copied to branches/release and replaces it.

### branches/release ###
Contains a development branch for the latest stable release version. Most of the time there is no activity, the branch stays available to quickly fix a critical bug that would be found in a release version.

To check out this branch:
```
svn checkout http://grafx2.googlecode.com/svn/branches/release/ stable
```
This creates a working copy in (new) directory _stable_.

#### Reporting fixes from release into trunk ####
After they're coded and packaged, the fixes can be reported back to trunk (so the next unstable version also benefits from the fixes). To do so:
  1. change directory to a working copy of trunk, and type:
```
svn merge https://grafx2.googlecode.com/svn/branches/release/
```
  1. Solve any conflicts (sometimes the fixes are already applied but differently)
  1. Check in.

#### New release ####
When the trunk is deemed stable, the release branch is upgraded to match its version:
  1. Change directory to a working copy of the release branch.
  1. Change the version label (remove "wip")
```
svn merge https://grafx2.googlecode.com/svn/branches/trunk/
```
  1. Solve any conflicts.
  1. Check in.
When done, you generally change the version label in trunk by adding 0.1 and "wip".
### wiki ###
It is possible to get the wiki content with svn. This makes it easier to upload a bunch of files (for example, images) to it than the online page editor.

To check out:
```
svn checkout http://grafx2.googlecode.com/svn/wiki/ wiki
```

You can edit existing pages from your working copy. You can also create new pages, but then please take care of linking them from other pages and not creating orphans.

### Creating a new branch ###
Create a branch `new_branch` starting as a copy of trunk on [revision 1034](https://code.google.com/p/grafx2/source/detail?r=1034) :

```
svn copy https://grafx2.googlecode.com/svn/trunk@1034 \
https://grafx2.googlecode.com/svn/branches/new_branch \
--username yrizoud -m "Commit message"
```