A very basic example to build a Processing library from scratch. Note that there are significant changes in 2.0 (starting with beta 7 in particular) to how events are handled.

```java
package libraryexample;
import processing.core.*;

public class BasicLibrary {
  PApplet parent;

  public BasicLibrary(PApplet parent) {
    this.parent = parent;
    parent.registerMethod("dispose", this);
  }

  public void dispose() {
    // Anything in here will be called automatically when 
    // the parent sketch shuts down. For instance, this might
    // shut down a thread used by this library.
  }
}
```

Usually you'll need to pass "this" to a library's constructor so that the library can access functions from PApplet, e.g. graphics methods like line() and stroke() or loadImage().

Using a static initializer such as ```javaYourLibrary.init(this)``` is discouraged because it's not a good way to write OOP code, and makes assumptions about how your library connects to a sketch, and it encourages bad style that implies a single instance of your library. If you need to share information across library instances, use static variables or methods behind the scenes, but don't expose them to the user through the initializer.


## Using PConstants

If you'd like to use constants such as RGB, use the following:

```java
public class BoringLibrary implements PConstants {
```

which will make all the constants available to that class.


## Subclassing PGraphics

Release 0148 included many changes to how libraries that implement PGraphics are handled. You can read about the changes in the developer's reference for PGraphics. Libraries that use the old PGraphics constructors will not work with release 0148 or later until these changes have been made to their API.

The changes may be a little confusing at first, but a quick look at the source to other PGraphics implementations, such as PGraphicsOpenGL or PGraphicsPDF should clarify the way the new methods are used.


## Library Methods

```java
public void pre()
```

Method that's called just after beginDraw(), meaning that it can affect drawing.

```java
public void draw()
```

Method that's called at the end of draw(), but before endDraw().

```java
public void post()
```

Method called after draw has completed and the frame is done. No drawing allowed.

```java
public void mouseEvent(MouseEvent e) 
```

Called when a mouse event occurs in the parent applet. Drawing is allowed because mouse events are queued, unless the sketch has called noLoop().

```java
public void keyEvent(KeyEvent e)
```

Called when a key event occurs in the parent applet. Drawing is allowed because key events are queued, unless the sketch has called noLoop().

```java
public void stop()
```

Called to halt execution. Can be called by users, for instance movie.stop() will shut down a movie that's being played, or camera.stop() stops capturing video. server.stop() will shut down the server and shut it down completely. May be called multiple times.

```java
public void dispose()
```

Called to free resources before shutting down. This should only be called by PApplet. The dispose() method is what gets called when the host applet is being shut down, so this should stop any threads, disconnect from the net, unload memory, etc.

```java
public void pause()
```

Called on Android when the sketch is paused (usually sent to the background).

```java
public void resume()
```

Called on Android when the sketch is resumed.

To register any of these methods with the parent, call parent.registerMethod("_methodname_", this), replacing _methodname_ with the name of the function (pre, draw, post, etc) that you'd like to use.

Note that making these methods "public" is extremely important. When running inside Processing, anything left blank has public added by the preprocessor, meaning "void draw()" actually becomes "public void draw()".


### When drawing (or code that manipulates a sketch) can occur

You can only draw inside of `pre()`, `draw()`, `mouseEvent()`, or `keyEvent()` otherwise you will run into problems. If using OpenGL to render, for instance, you can easily make your machine (or at least the sketch) crash hard if you mess with the drawing surface when you're not supposed to. `pre()` and `draw()` happen while legitimate drawing is taking place, and the mouse/key events happen just before `draw()` events are called, they're queued up by the host applet until it's safe to draw. The exception is when `noLoop()` has been called, and events have to fire immediately (otherwise a sketch wouldn't be able to restart itself on key or mouse input). 

For this reason, you should use `registerMethod("mouseEvent")` and `mouseEvent()` (and same for the keys) to handle your events, rather than your class implementing `MouseListener` from Java's AWT. (In addition, AWT is not available with OpenGL, nor with Android, so your code wouldn't work properly there.) 

Note that method `mouseEvent(MouseEvent event)` has a parameter of type [MouseEvent](http://processing.org/reference/javadoc/core/processing/event/MouseEvent.html) (javadoc link). Because the `MouseEvent` is a subclass of `processing.event.Event` it is independent from Java's AWT.

To figure out what the mouse event is throwing back at you, this would be an example handler:

```java
public void mouseEvent(MouseEvent event) {
  int x = event.getX();
  int y = event.getY();

  switch (event.getAction()) {
    case MouseEvent.PRESS:
      // do something for the mouse being pressed
      break;
    case MouseEvent.RELEASE:
      // do something for mouse released
      break;
    case MouseEvent.CLICK:
      // do something for mouse clicked
      break;
    case MouseEvent.DRAG:
      // do something for mouse dragged
      break;
    case MouseEvent.MOVE:
      // do something for mouse moved
      break;
  }
}
```

Check out the code and API for the processing.event package for more advanced features. And again, as of 2.0b7, these are no longer AWT events, so you cannot use AWT methods on them.


## Structure of a Library Folder

The ancient [Sonia library](http://sonia.pitaru.com/) by Amit Pitaru is a fine (if no longer supported) example here. To make a library called sonia, you create a folder called `sonia` and within that, a subfolder named `library`. The `sonia` folder should be placed inside the Processing `libraries` folder, or a user can place it inside their sketchbook folder.

Inside `library`, you'll find `sonia.jar`. Anything that is found inside `library` will be exported with your sketch. For Sonia, the files are laid out as follows:

```
/sonia.zip/sonia/library/export.txt
/sonia.zip/sonia/library/sonia.jar
/sonia.zip/sonia/library/JSynClasses.jar
/sonia.zip/sonia/library/JSynV142.dll
/sonia.zip/sonia/library/libJSynV142.jnilib
```

If different sets of files should be exported with applets versus applications, you have two options. You can create a file called `export.txt` that specifies files to export for different scenarios, or you can create separate folders for each operating system your library supports and partition the files accordingly.

### Using export.txt

Sonia uses an `export.txt` file, which looks like this:

```
# only export the jar file for applets..
# everything else is installed as a separate browser plugin
applet=sonia.jar
# application needs everything
application=sonia.jar,JSynClasses.jar,JSynV142.dll,libJSynV142.jnilib
```

This will include sonia.jar for applets, because in a web browser, the DLL files must be installed separately along with `JSynClasses.jar`. The # sign in front of a line means that the line is a comment, and it'll be ignored by the PDE.

As of revision 0097, you can also specify what to export for other platforms as well (at least Mac OS X, Windows, Linux). For the example above, the application line could instead be changed to:

```
application.macosx=sonia.jar,JSynClasses.jar,libJSynV142.jnilib
application.windows=sonia.jar,JSynClasses.jar,JSynV142.dll
```

Platform-specific exports will be checked first, and if they don't exist, the `application` line will be used. If neither exist (or `export.txt` doesn't exist), the entire contents of the `library` folder will be copied during export.

You can optional further differentiate between 32 and 64 bit systems by appending 32 or 64 to the property. For example, if Sonia had a special DLL for working with 64 bit Windows, the `export.txt` file might look as follows:

```
application.windows=sonia.jar,JSynClasses.jar,JSynV142.dll
application.windows64=special64stuff.dll
```

In this example, the PDE on 64 bit Windows would export `special64stuff.dll` in addition to exports listed in `applications.windows`, and for 32 bit Windows, it would only export files from the `application.windows` list.

### Specifying exports using folders alone

When possible, it's better to use folders to determine which files are copied. In this case, no `export.txt` file is necessary. For instance:

```
/sonia.zip/sonia/library/sonia.jar
/sonia.zip/sonia/library/macosx/JSynClasses.jar
/sonia.zip/sonia/library/macosx/libJSynV142.jnilib
/sonia.zip/sonia/library/windows/JSynClasses.jar
/sonia.zip/sonia/library/windows/JSynV142.dll
/sonia.zip/sonia/library/windows64/JSynClasses.jar
/sonia.zip/sonia/library/windows64/JSynV142.dll
/sonia.zip/sonia/library/windows64/special64stuff.dll
```

As with the properties in the `export.txt` file, these can be optionally separated to distinguish exports between 32 and 64 bit versions of an operating system. However, only one folder will ever be used at a time for the classpath. This means that if you provide a specific `library/windows64` folder, the `library/windows` folder will not be used when exporting applications for 64 bit Windows.

## <a name='DescribingYourLibrary'/>Describing Your Library – library.properties</a>

Processing 2.0+ supports installing libraries from within the PDE using the Contribution Manager. To make the installation of your library possible, you must add a file named `library.properties` to the base directory of your library. For example, if we were to extract `sonia.zip`, we should see the following file structure:

```
sonia/library.properties
sonia/library/sonia.jar
...
```

In `library.properties`, you should include the following attributes:

```
# UTF-8 supported.

# The name of your library as you want it formatted.
name = Most Pixels Ever

# List of authors. Links can be provided using the syntax [author name](url).
authors = [Daniel Shiffman](http://www.shiffman.net/) and Chris Kairalla

# A web page for your library, NOT a direct link to where to download it.
url = http://www.mostpixelsever.com/

# The category (or categories) of your library, must be from the following list:
#   "3D"            "Animation"     "Compilations"      "Data"          
#   "Fabrication"   "Geometry"      "GUI"               "Hardware"      
#   "I/O"           "Language"      "Math"              "Simulation"    
#   "Sound"         "Utilities"     "Typography"        "Video & Vision"
# 
# If a value other than those listed is used, your library will listed as 
# "Other". Many categories must be comma-separated.
categories = Hardware

# A short sentence (or fragment) to summarize the library's function. This will 
# be shown from inside the PDE when the library is being installed. Avoid 
# repeating the name of your library here. Also, avoid saying anything redundant 
# like mentioning that it's a library. This should start with a capitalized 
# letter, and end with a period.
sentence = Framework for spanning Processing sketches across multiple screens.

# Additional information suitable for the Processing website. The value of
# 'sentence' always will be prepended, so you should start by writing the
# second sentence here. If your library only works on certain operating systems,
# mention it here.
paragraph =  

# Links in the 'sentence' and 'paragraph' attributes can be inserted using the
# same syntax as for authors. 
# That is, [here is a link to Processing](http://processing.org/)

# A version number that increments once with each release. This is used to 
# compare different versions of the same library, and check if an update is 
# available. You should think of it as a counter, counting the total number of 
# releases you've had.
version = 22  # This must be parsable as an int

# The version as the user will see it. If blank, the version attribute will be 
# used here. This should be a single word, with no spaces.
prettyVersion = 0.98a  # This is treated as a String

# The min and max revision of Processing compatible with your library.
# Note that these fields use the revision and not the version of Processing, 
# parsable as an int. For example, the revision number for 2.2.1 is 227. 
# You can find the revision numbers in the change log: 
# https://raw.githubusercontent.com/processing/processing/master/build/shared/revisions.txt
# Only use maxRevision (or minRevision), when your library is known to 
# break in a later (or earlier) release. Otherwise, use the default value 0.
minRevision = 0
maxRevision = 227
```

## Advertising Your Library

Starting with Processing 2.0, libraries that are advertised on [Processing's website](http://processing.org/reference/libraries/) also have the option of being advertised through the PDE. To support this, you'll need to include a `library.properties` file with your library and make a few changes to how it's hosted on your server.

You must include the following attributes in `library.properties`: 
* `name`
* `authors`
* `url`
* `categories`
* `sentence`
* `version`

You should also set the `minRevision` and `maxRevision` attributes to indicate the Processing revisions compatible with your library. Note that these fields use the [revision](https://raw.githubusercontent.com/processing/processing/master/build/shared/revisions.txt) and not the version of Processing (e.g. the revision number for 2.2.1 is 227). Only use `maxRevision` (or `minRevision`), when your library is known to break in a later (or earlier) release. Otherwise, use the default value `0`.

You will need to provide a static link to the latest version of your library, and host a copy of your `library.properties` alongside it. The result on your server should look something like this:

```
http://www.example.com/awesomelib.zip (The latest version of awesomelib)
http://www.example.com/awesomelib.txt (A copy of the library.properties file contained in awesomelib.zip)
```

Once everything is in place, send your static links to the Processing Librarian: [Elie Zananiri](mailto:prisonerjohn+p5@gmail.com). We'll review your properties file to make sure everything is in order and add your contribution to the list of advertised libraries.

On our end, we'll only record the location of `awesomelib.txt`, and we'll assume that a copy of the library file is hosted at an address by the same name, except ending in `zip`. Each day, a script on processing.org will scrape the information from all the .txt files and aggregate it into a single file, which is then used by each user to browse what's available and check for updates. Even if your library is not being advertised, you should still include the `library.properties` file inside your zip.

## Releasing An Update

When you want to release a new version of your library, here's what you'll need to do:

### Option 1: Manual Update
1. Update your `library.properties` file inside your `.zip`
  * Increment the value of `version`. This is an integer that we'll use to check for updates. You can think of it as a counter, counting the total number of releases you've had.
  * Write whatever you want for the new value of `prettyVersion` (as long as it's a single word with no spaces).
1. Copy your latest release to the static address you gave us earlier (e.g. http://www.example.com/awesomelib.zip)
1. Copy the `library.properties` file from your latest release to a `.txt` file hosted at an address by the same name as your `.zip`, except instead ending in `.txt` (e.g. http://www.example.com/awesomelib.txt)

### Option 2: Update using the [Processing Library Template for Eclipse](https://github.com/processing/processing-library-template)
1. Update your `build.properties` file from the `resources` folder.
  * Increment the value of `library.version`. This is an integer that we'll use to check for updates. You can think of it as a counter, counting the total number of releases you've had.
  * Write whatever you want for the new value of `library.prettyVersion` (as long as it's a single word with no spaces).
1. Recompile the project using the Ant script. This will generate the appropriate files in the `distribution/name-version/download` folder.
1. Copy your latest release and properties files to the static address you gave us earlier (e.g. http://www.example.com/awesomelib.zip and http://www.example.com/awesomelib.txt)

That's it. The next time the aggregator script runs and your users start the PDE, they'll be notified that updates are available.

## Using Other Java Code as a Library

So long as the code is inside a package, it can be set up for use as a library. For instance, if you want to make a library called `poo` set up a folder as follows:

```
poo →
  library →
    poo.jar
```

Then, the folder should be placed in the libraries folder inside the user's sketchbook folder to be recognized by Processing and its "Import Library" menu. You must first restart Processing in order to use the library.

While this process may sound a little complicated, the intent is to make it easier for users than a typical Java IDE. A little added complexity for the developers of library code (who will generally be more advanced users) is traded for great simplicity by the users, since Processing is intended to target beginning programmers.


## Import Statements and How They Work

If your library is `sonia.jar`, found at `sonia/library/sonia.jar`, all the packages found in `sonia.jar` will be added as imports into the user's sketch when they selected "Import Library".

In the case of Sonia, an additional JAR file can be found in the `sonia/library/` folder, `jsyn.jar`. The contents of `jsyn.jar` will not be added to the import statements. This is to avoid every library having a ridiculously large number of import statements. For instance, if you want to use the video library, you don't want all 15-20 packages for the QuickTime libraries listed there to confuse your users.

Bottom line, if you want packages from the other JARs to be loaded by Processing, then you need to put those `.class` files into the main `.jar` file for the library (`sonia/library/sonia.jar` in this case).


## Creating .jar Files For Your Library

Since your code is inside a package, you need to make sure that it's inside subfolders in the `.jar` file. It should be noted that JAR files are simply `.zip` files (they can be opened with WinZip or Stuffit) with a "manifest" file.

In the past, you may have used:

```
javac *.java
```

to compile your files. Once they're inside a packages, you must use:

```
javac -d . *.java
```

which will create folders and subfolders for the packages. For instance, for all the stuff in `processing.core.*` it would create:

```
processing/ ->
  core/ ->
    PApplet.class
    PGraphics.class
    ..etc
```

then you can jar that stuff up using:

```
jar -cf core.jar processing
```

or with a command line zip utility:

```
zip -r core.jar processing
```

## The "Import Library" Menu Item

All "Import Library" does is add the `import yourlibrary.*`; statement to the top of your sketch. If you've handwritten the import statements, then there's no need to use "Import Library".


## Adding Your Own Library Events

So that your library can notify the host applet that something interesting has happened, this is how you implement an event method in the style of `serialEvent`, `serverEvent`, etc.

```java
import java.lang.reflect.*;

public class FancyLibrary {
  Method fancyEventMethod;

  public FancyLibrary(PApplet parent) {
    // your library init code here...

    // check to see if the host applet implements
    // public void fancyEvent(FancyLibrary f)
    try {
      fancyEventMethod =
        parent.getClass().getMethod("fancyEvent",
                                    new Class[] { FancyLibrary.class });
    } catch (Exception e) {
      // no such method, or an error.. which is fine, just ignore
    }
  }

  // then later, to fire that event
  public void makeEvent() {
    if (fancyEventMethod != null) {
    try {
      fancyEventMethod.invoke(parent, new Object[] { this });
    } catch (Exception e) {
      System.err.println("Disabling fancyEvent() for " + name +
                         " because of an error.");
      e.printStackTrace();
      fancyEventMethod = null;
    }
  }
}
```

## Using Built-in Functions From processing.core

Many methods in `PApplet` are made static for use by other libraries and code that interfaces with Processing. For instance, `createInput()` requires an applet object, but there's a version of `loadStrings() `that is a static method that can be run on any `InputStream`. See the developer's reference for more information about which methods are available.

## Accessing Files From Inside a Library

To open files for use with a library, use the `createInput()` method. This is the most compatible means for loading data, and makes use of many hours of headaches that were the result of attempts to create functions that loaded data across platforms (Mac, Windows, and Linux) and circumstances (applet, application, and other). Similarly, to get an `OutputStream` for writing files, use `createOutput()`.

The functions `sketchPath()`, `sketchFile()`, `savePath()`, `dataPath()`, and `createPath()` also facilitate reading and writing files relative to the sketch folder. They should be used to ensure that file I/O works consistently between your library and functions like `loadImage()` or `loadStrings()`. Their documentation can be seen as part of the developer's reference for `PApplet`. The variable `sketchPath` is also available for convenience, but in nearly all cases, the `sketchPath()` method is a better (and more compatible) route. The `sketchFile()` method works like `sketchPath()`, except that it wraps the path as a `java.io.File` object instead of the full path as a `String`.


## Getting an !UnsupportedClassVersionError?

Processing currently uses Java 1.6. If you compile your library code with a later Java release, it may be incompatible with the Java 1.6 class file format, which will give users a message like the following:

```
java.lang.UnsupportedClassVersionError: blah/SomeClass (Unsupported major.minor version 49.0)
```
 
This is because later versions of Java use their own class file format that's not backwards compatible.

When compiling a library, use something like:

```
javac -source 1.6 -target 1.6 -d . -classpath /path/to/core.jar path/to/java/source/*.java
```

## Library Naming Rules

Libraries, or classes inside them, should not be prefixed with "P" the way that the core Processing classes are (`PImage`, `PGraphics`, etc). It's tempting to prefix everything that way to identify it with Processing, but we'd like to reserve that naming for "official" things that are inside `processing.core` and other associated classes.

Same goes for using "Processing", "Pro", or "P5" just like "P", or whether it's a prefix or a suffix.

If, however, your library is a Processing port of or a bridge to another framework, you can name it something along the lines of "XXX for Processing". 

Similarly, please don't use `processing` as the prefix for your library packages. We'd like to keep that name space clear for official things as well. 