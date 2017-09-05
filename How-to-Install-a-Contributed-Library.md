## Install with the "Add Library..." tool

For Processing versions 2.0 and up, add contributed libraries by selecting "Add
Library..." from the "Import Library..." submenu within the Sketch menu.
Not all available libraries have been converted to show up in this menu.
If a library isn't there, it will need to be installed manually by
following the instructions below.

## Manual Install

Prior to Processing 2.0, it was necessary to add libraries manually. Only follow the Manual Install instructions here if you are using an older version of the software or if the library you want to add isn't included in the "Add Library..." list mentioned above.

Contributed libraries may be downloaded separately and manually placed
within the *libraries* folder of your Processing sketchbook. As a
reminder, the sketchbook is where your sketches are saved. To find (and
change) the Processing sketchbook location on your computer, open the
Preferences window from the Processing application (PDE) and look for
the "Sketchbook location" item at the top.

Copy the contributed library's folder into the *libraries* folder at
this location. You will need to create the *libraries* folder if this
is your first contributed library.

By default the following locations are used for your sketchbook folder.
For Mac users the sketchbook folder is located inside
`~/Documents/Processing`. For Windows users the sketchbook folder is
located inside folder `Documents/Processing`.

Let's say you downloaded a library with name *theLibrary*. Then the
folder structure of this library inside the *libraries* folder should
look like the one below. The top folder of a library must have the same
name as the .jar file located inside a library's *library* folder
(minus the .jar extension):

```
     Documents
           Processing
                 your sketch folders
                 libraries
                       theLibrary
                             examples
                             library
                                   theLibrary.jar
                             reference
                             src
```

Some folders like examples or src might be missing. After a library has
been successfully installed, restart Processing application.

## Still having trouble?


In some cases the top folder of a library does not exist after
extracting from the downloaded zip file. In this case, the top folder
must be created manually and given the same name as the .jar file inside
folder library. After creating and renaming the top folder, move all
extracted folders from the zip file in there.

For example, you downloaded the library *otherLibrary*, and the folder
structure in the zip file looks like this:

```
     examples
     library
           otherLibrary.jar
           auxiliary.jar
     documentation
     src
```

You must create the *otherLibrary* folder in the *libraries* folder
and copy the above folders inside, resulting in a structure like this:

```
     Documents
           Processing
                 your sketch folders
                 libraries
                       otherLibrary
                             examples
                             library
                                   otherLibrary.jar
                             documentation
                             src
```

After a library has been successfully installed, restart Processing
application.

## Non-Processing Libraries

Another example: you want to use the Apache Common Collections library,
which is a plain Java library (ie. not designed for use with
Processing). The zip file contains a folder named
commons-collections-3.2.1 with various files in it, including one:
commons-collections-3.2.1.jar

You have to create the libraries/ApacheCommonCollections/library folder
(the middle name can vary, but must have only letters and numbers) where
you put the jar file renamed along the folder name (here,
ApacheCommonCollections.jar, then).

Alternatively, if you need this library for only one sketch, you can
just drag'n'drop the jar file on the PDE, it will put it in a folder
named `code` in the sketch folder (you can also create the folder
manually and put the jar file there yourself). This also works, of
course, for regular Processing libraries. This solution isn't optimal if
you plan to use the library in several sketches, as it will duplicate
the library, taking up space and making difficult a possible upgrade.
