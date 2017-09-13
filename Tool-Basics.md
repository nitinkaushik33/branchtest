What follows is a very basic example to build a Processing tool from scratch. This sample tool replaces the contents of the current sketch tab with an obnoxious message:

```java
package toolexample;

import processing.app.Editor;

public class DestructiveTool implements Tool {
  Base base;

  // In Processing 3, the "Base" object is passed instead of an "Editor"
  public void init(Base base) {
    // Store a reference to the Processing application itself
    this.base = base;
  }
  
  public void run() {
    // Run this Tool on the currently active Editor window
    Editor editor = base.getActiveEditor();
    editor.setText("Deleted your code. What now?");
  }
  
  public String getMenuTitle() {
    return "A Destructive Tool";
  }
}
```

Remember to compile the tool with compliance to java version 1.7 or 1.8 (`javac -source 1.7 -target 1.7`) or your Tool will not load properly.

All tools must implement the `Tool` interface from the `processing.core.app.tools` package. It's important to note that in order for an exported tool to appear in the Tools menu, the class implementing `Tool` cannot reside in the default package.

If you're unfamiliar with the concept of interfaces or inheritance in object oriented programming, refer to [the Java tutorial](https://docs.oracle.com/javase/tutorial/). When a class "implements" an interface it allows other code to make assumptions about how that class works. The `Tool` interface prescribes three methods and is defined as follows:

```java
package processing.app.tools.Tool;

public interface Tool extends Runnable {

  public void init(Base base);

  public void run();

  public String getMenuTitle();
  
}
```

## Tool Methods

```java
public void init(Base base)
```
This method is called when the first Processing Editor window opens. This means you won't have access to a sketch object, or a GUI, and should only do minimal setup. You should store the `base` object so that you can get the current Editor object from inside your `run()` method. 

Prior to Processing 3 (beta 6), each Tool was loaded once per Editor window. This used a lot of memory and made things slow. We've changed that, and in beta 7 the API was changed to pass the `Base` object around. Use the `getActiveEditor()` method to get the frontmost window. However, do not store that Editor object in your class, otherwise you'll cause a memory leak. It should live as a local variable inside your `run()` method.

```java
public void run()
```
This method will be called by the main application when the tool is selected from the menu. This is called using `EventQueue.invokeLater()`, so that the tool can safely use Swing or any other GUI.

Keep in mind that `run()` is called *every time* the tool is selected from the menu. Thus if your sketch is creating a window, a frame or sets up a timer, you need to make sure that you do your initialization only once.

If your tool needs to open a window, you may want to use the `Frame` class from the `java.awt` package. The first time `run()` is called you'll create the `Frame` object. Subsequent calls to `run()` should check to see if the `Frame` is still open. If it is, the `Frame` should be brought to the front of the screen. If not, a new `Frame` should be created. This ensures the user won't create superfluous instances of your tool's window(s).

You can really do anything in the `run()` method. In lieu of opening a new window, you can use the `statusNotice()` and `statusError()` methods in Editor to let the user know what's happened. See below for a list of Processing classes sanctioned for use in Tool development.

```java
public String getMenuTitle()
```
This method simply returns the title for what should appear in the Tools menu. Typically the body for this method looks something like `return "Tool Name";`. Ordering in the Tools menu is alphabetical.

We've yet to implement shortcut assignment for contributed tools. Resolving keystroke collisions between user contributed tools and the rest of the environment is [tougher than it might appear](https://github.com/processing/processing/issues/83).

## What Tools Can and Cannot Do

The following classes have been sufficiently documented for use in `Tool` classes:


[`processing.app.Base`](https://github.com/processing/processing/blob/master/app/src/processing/app/Base.java)

The base class for the main Processing application.

[`processing.app.ui.Editor`](https://github.com/processing/processing/blob/master/app/src/processing/app/ui/Editor.java)

Main editor panel for the Processing Development Environment.

[`processing.app.Preferences`](https://github.com/processing/processing/blob/master/app/src/processing/app/Preferences.java)

Storage class for user preferences and environment settings.

[`processing.app.Sketch`](https://github.com/processing/processing/blob/master/app/src/processing/app/Sketch.java)

Stores information about files in the current sketch

[`processing.app.SketchCode`](https://github.com/processing/processing/blob/master/app/src/processing/app/SketchCode.java)

Represents a single tab of a sketch.

For the most part, your code should use the methods provided by the Editor API. Of course, you're welcome to explore the documentation and leverage objects that Editor's methods might return (most notably `JEditTextArea`). Developers should use caution when accessing/manipulating these objects as they might disrupt existing PDE interface elements or features. 

## Structure of a Tool Folder

Tools should be distributed as zipped files, and the distribution should be laid out as follows:
```
MyTool/tool/MyTool.jar
MyTool/src/
```
The `tool` folder contains the tool's `.jar` file (and if necessary, any additional `.jar`, `.dll`, `.so`, or `.jnilib` files). The name of the outermost folder must conform to the name of the class implementing the `Tool` interface. The name of the JAR contained in `/tool/` must have the same name as the outermost folder. When Processing loads, the JAR will be searched for `MyToolClass.class`. Once again, package names are required.

See the [Eclipse Tool Template](https://github.com/processing/processing-templates/wiki/Eclipse-Tool-Template) for information on compiling a JAR for your tool.

## Describing Your Tool – tool.properties

Processing 2.0+ will support installing tools from within the PDE using the Contribution Manager. To make the installation of your tool possible, you must add file named `tool.properties` to the base directory of your tool. For example, if we were to extract `ColorSelectorPlusTool.zip`, we should see the following file structure:
```
ColorSelectorPlusTool/tool.properties
ColorSelectorPlusTool/tool/ColoSelectorPlusTool.jar
```
In `tool.properties`, you should include the following attributes:
```
# UTF-8 supported.

# The name of your tool as you want it formatted.
name = HelloTool

# List of authors. Links can be provided using the syntax [author name](url).
authors = [Your Name](http://yoururl.com)

# A web page for your tool, NOT a direct link to where to download it.
url = http://yourtoolname.com

# The category (or categories) of your tool, must be from the following list:
#   "3D"            "Animation"     "Compilations"      "Data"          
#   "Fabrication"   "Geometry"      "GUI"               "Hardware"      
#   "I/O"           "Language"      "Math"              "Simulation"    
#   "Sound"         "Utilities"     "Typography"        "Video & Vision"
# 
# If a value other than those listed is used, your library will listed as 
# "Other". Many categories must be comma-separated.
categories = Other

# A short sentence (or fragment) to summarize the tool's function. This will be
# shown from inside the PDE when the tool is being installed. Avoid repeating
# the name of your tool here. Also, avoid saying anything redundant like
# mentioning that it's a tool. This should start with a capitalized letter, and
# end with a period.
sentence = A collection of utilities for solving this and that problem.

# Additional information suitable for the Processing website. The value of
# 'sentence' always will be prepended, so you should start by writing the
# second sentence here. If your tool only works on certain operating systems,
# mention it here.
paragraph =  

# Links in the 'sentence' and 'paragraph' attributes can be inserted using the
# same syntax as for authors. 
# That is, [here is a link to Processing](http://processing.org/)

# A version number that increments once with each release. This is used to 
# compare different versions of the same tool, and check if an update is 
# available. You should think of it as a counter, counting the total number of 
# releases you've had.
version = 1  # This must be parsable as an int

# The version as the user will see it. If blank, the version attribute will be 
# used here. This should be a single word, with no spaces.
prettyVersion = 0.1.1  # This is treated as a String

# The min and max revision of Processing compatible with your tool.
# Note that these fields use the revision and not the version of Processing, 
# parsable as an int. For example, the revision number for 2.2.1 is 227. 
# You can find the revision numbers in the change log: https://raw.githubusercontent.com/processing/processing/master/build/shared/revisions.txt
# Only use maxRevision (or minRevision), when your tool is known to break in a 
# later (or earlier) release. Otherwise, use the default value 0.
minRevision = 0
maxRevision = 227
```
## Advertising Your Tool
Starting with Processing 2.0, tools that are advertised on [Processing's website](http://processing.org/reference/tools) also have the option of being advertised through the PDE. To support this, you'll need to include a `tool.properties` file with your tool and make a few changes to how it's hosted on your server.

First, you must include the following attributes in `tool.properties`: 
* `name`
* `authors`
* `url`
* `categories`
* `sentence`
* `version`

You should also set the `minRevision` and `maxRevision` attributes to indicate the Processing revisions compatible with your tool. Note that these fields use the [revision](https://raw.githubusercontent.com/processing/processing/master/build/shared/revisions.txt) and not the version of Processing (e.g. the revision number for 2.2.1 is 227). Only use `maxRevision` (or `minRevision`), when your tool is known to break in a later (or earlier) release. Otherwise, use the default value `0`.

You'll also need to provide a static link to the latest version of your tool, and host a copy of your `tool.properties` alongside it. The result on your server should look something like this:
```
http://www.example.com/awesometool.zip/ (The latest version of awesometool)
http://www.example.com/awesometool.txt/ (A copy of the tool.properties file contained in awesometool.zip)
```
Once everything is in place, send your static links to the Processing Librarian: [Elie Zananiri](mailto:prisonerjohn+p5@gmail.com). We'll review your properties file to make sure everything is in order and add your contribution to the list of advertised tools.

On our end, we'll only record the location of `awesometool.txt`, and we'll assume that a copy of the tool file is hosted at an address by the same name, except ending in `zip`. Each day, a script on processing.org will scrape the information from all the .txt files and aggregate it into a single file, which is then used by each user to browse what's available and check for updates. Even if your tool is not being advertised, you should still include the `tool.properties` file inside your zip.

## Releasing An Update

When you want to release a new version of your tool, here's what you'll need to do:

### Option 1: Manual Update
1. Update your `tool.properties` file inside your `.zip`
  * Increment the value of `version`. This is an integer that we'll use to check for updates. You can think of it as a counter, counting the total number of releases you've had.
  * Write whatever you want for the new value of `prettyVersion` (as long as it's a single word with no spaces).
1. Copy your latest release to the static address you gave us earlier (e.g. http://www.example.com/awesometool.zip)
1. Copy the `tool.properties` file from your latest release to a `.txt` file hosted at an address by the same name as your `.zip`, except instead ending in `.txt` (e.g. http://www.example.com/awesometool.txt)

### Option 2: Update using the [Eclipse Tool Template](https://github.com/processing/processing-templates/wiki/Eclipse-Tool-Template)
1. Update your `build.properties` file from the `resources` folder.
  * Increment the value of `tool.version`. This is an integer that we'll use to check for updates. You can think of it as a counter, counting the total number of releases you've had.
  * Write whatever you want for the new value of `tool.prettyVersion` (as long as it's a single word with no spaces).
1. Recompile the project using the Ant script. This will generate the appropriate files in the `distribution/name-version/download` folder.
1. Copy your latest release and properties files to the static address you gave us earlier (e.g. http://www.example.com/awesometool.zip and http://www.example.com/awesometool.txt)

That's it. The next time the aggregator script runs and your users start the PDE, they'll be notified that updates are available.