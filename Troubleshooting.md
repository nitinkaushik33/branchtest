Having a problem? Hopefully the information on this page will help.

### I've found a bug!

Please use the [forum](https://forum.processing.org) for general troubleshooting questions, especially if it's something like Processing not starting up properly, or sketches not running. 

#### What To Do

* First, read through this page. 
* Second, also check the [Supported Platforms](Supported_Platforms "wikilink") page 
in case it's something specific to your operating system.
* Third, check [the Forum](http://forum.processing.org). The Forum is the place for 
  "this isn't working" type questions. 
* Fourth, search the [bug
database](https://github.com/processing/processing/issues?state=open) to
see if your problem has already been reported. 

#### What Not To Do

Please do not:
* Submit an issue saying "Processing is broken" or "Processing won't start". That's not helpful (see below).
* Reinstall Java, it [does nothing](https://github.com/processing/processing/wiki/Supported-Platforms#java-versions) and just adds to the noise.

#### If it's a bug

If you don't find your problem, [submit a new issue here](https://github.com/processing/processing/issues/new).

When reporting please include information about

1.  The version number (i.e. 3.1.2)
2.  The operating system you're using (Windows, Mac, Linux, etc.), 
    and on what kind of hardware
3.  A copy of the smallest possible piece of code that will produce the error
4.  Details of the error, like the red spew that you see in the console.
5.  Only one issue per report! Each issue should be one... issue. It's not a point-by-point 
    letter for the development team. If you have multiple issues, file them separately.
    If multiple issues are in one report, it'll be closed.

For best results:

* Write a useful title for the report. "Processing broken" or "visual problem" 
  are dreadful titles. The first one isn't helpful because you're reporting an 
  issue, so we already know you think Processing is broken. Saying "visual problem" 
  isn't helpful because Processing is used to make visual things, so nearly *all* 
  problems are "visual" problems.
* The people receiving this report work on Processing in their free time because
  they think it's important for the community. Berating or insulting them is 
  obnoxious, demotivating, and a good way to ensure that your report is ignored. 
  
For stranger errors during compile time, you can also look inside the
build folder which contains an intermediate (translated into Java)
version of your code. The build folder will be located inside a
temporary directory on your machine, probably /tmp/buildNNNN on Mac OS X
and Linux, or on Windows, in one of its many "TEMP" folders, inside a
buildNNNN folder (the Ns will be numbers or letters). The more details
you can post, the better, because it helps us figure out what's going
on. Useful things when reporting:

-   We want the minimum amount of code that will still replicate the
    bug. The worst that can happen is we get a report with a subject
    saying "problem!" along with a three page program. Sure, everyone
    likes a puzzle, but simpler code will receive a faster response.
-   Occasionally we may need you to pack up a copy of your sketch folder
    or something similar so that we can try and replicate the weirdness
    on our own machine. Rest assured, we have no interest in messing
    with your fancy creations or stealing your ideas. The Processing
    team is a pair of straight-laced boys who hail from the midwestern
    U.S. who were brought up better than that. And as we often lack
    enough time to build our own projects, we have even less time to
    spend figuring out other peoples' projects to rip them off.

### Processing won't start! Nothing (or something strange) happens when I click “Run”!

**All Platforms**

-   Please first seek help on the [Processing Forum](http://forum.processing.org). 
    We've tested the releases and thousands of people are able to start Processing. 
    If you find that a specific Tool, Mode, or Library is the problem after
    following the steps below please write to the author of that extension.

-   Try moving or renaming your Sketchbook. Sometimes a Mode or Tool
    conflicts with opening Processing. This will disable all Modes and
    Tools and a new Sketchbook will be created in the default location.
    Once Processing is opening again, code can be moved back into the
    new Sketchbook.
    -   The sketchbook on Windows XP is Documents and Settings →
        username → Application Data → Processing.
    -   On Windows 7 and later, it's Users → username → AppData →
        Roaming → Processing.
    -   For Mac OS X, it's Users → username → Library → Processing.

-   An alternate approach to moving or renaming the Sketchbook is to
    change the name of each Mode and Library inside the Sketchbook one
    at a time. When the name of the Mode or Library that is causing the
    issue is changed, Processing will start and you'll know where the
    issue is.

-   Errors inside code that is outside of setup() or draw() may just
    hang/freeze Processing. For instance, with this code, if "blah.vlw"
    is not in the "data" folder, it may just hang (and won't work in any
    case). Never use loadXxxx() methods outside setup() and draw().

    ``` {.processing}
    PFont font = loadFont("blah.vlw");
    
    void setup {
      // your awesome code
    }
    ```

**Windows**

-   Try deleting your preferences file. On Windows XP this is located in
    Documents and Settings → username → Application Data → Processing →
    preferences.txt. On Windows 7 and later, it's in Users → username →
    AppData → Roaming → Processing → preferences.txt. Sometimes a bad
    preferences file can prevent the application from running. If you've
    recently hand-edited preferences.txt, that's also a likely suspect.
    Only delete the preferences file when Processing is not running. And
    do not modify the preferences.txt file inside the Processing "lib"
    folder.

-   Next try running from a command prompt with the following:
    > .\\processing.exe --l4j-debug

    This will create a launch4j.log file which will describe what's
    happening during the startup. Then you can post on the discourse
    section of the site to inquire for help, or the bugs database if you
    think it's a bug.

-   An exceptionally large sketchbook folder (especially on a slower
    machine/disk) can sometimes cause startup problems. The launcher
    starts, but times out because it assumes something is broken (the
    Processing code is still indexing the sketchbook) and says there's a
    launch4j error.

-   If you're having trouble with P2D or P3D (which use OpenGL
    graphics), update your graphics drivers. This is almost always the
    cause of problems in P2D and P3D.

-   Try disabling any overly protective virus scanning software. It
    might be holding things up, especially when libraries have been
    imported.

**Mac OS X**

-   Make sure your version of OS X is supported. See the [Supported
    Platforms](Supported Platforms "wikilink") page for more
    information.

-   Open Console.app, found in Applications → Utilities → Console.app
    and see if there are any messages. If you don't know what they mean,
    post them to the [forum](http://forum.processing.org) where someone
    can help you out.

-   For weird hangs/nothing happening on startup. Do the following: 

    Open Applications → Utilities → Terminal.app

    Assuming you have Processing installed in Applications, type: 
    ```
    cd /Applications
    ./Processing.app/Contents/MacOS/Processing 
    ```
    If that prints any error messages, report them on the Forum or
    as a new issue so that we can help troubleshoot the problem and
    prevent it in the future.

**Linux**

See the Linux section of [Supported
Platforms](Supported Platforms "wikilink") for additional notes.

### This used to work and now it doesn't

Read the [Changes](Changes "wikilink") section of the reference.

#### Other Common Problems

-   Another common problem is placing images or files into the sketch
    folder by hand, rather than placing them in the data folder (or
    using "Add File..." to do so automatically). This will work from the
    PDE, but on export, the files won't be in included with your sketch
    because they're not in the data folder.

-   Watch out for issues with capitalization! Windows and Mac OS don't
    care about capitalization, so "blah.JPG" looks just the same as
    "blah.jpg". However, since most servers run on Unix, capitalization
    becomes a huge problem, because it must be exact. We've added some
    checks to try and catch this (at least for images) but they're not
    perfect. This can especially be a problem when the .JPG extension is
    not even visible (the default on Windows), so you don't know whether
    it's upper or lower case.

### Out Of Memory Errors (java.lang.OutOfMemoryError)

If you get an `OutOfMemoryError` while running your program, use the
Preferences window to increase the amount of available memory. Check the
box next to "Increase maximum available memory" and enter an amount.

Depending on your OS and available RAM, there are limits on how much
memory you can ask for.

32-bit operating systems and software are usually limited to addressing
somewhere around either 2GB and 4GB of RAM at a time. This means that
even if you have 8GB of RAM installed in your machine, you may only be
able to use shy of 2GB per application. Most Windows systems seem to be
limited to 2 or 3GB, while Mac OS X and Linux can usually access shy of
4GB. Upcoming 64-bit operating systems get around this restriction and
increase the amount of available memory significantly. However, even if
you're running a 64-bit OS like Mac OS 10.5, or a 64-bit Linux, a
combination of factors (version of Java, etc.) may mean that you're
still limited by the 32-bit boundary of 2GB or 4GB.

*Use this preference with caution,* because if you set the memory too
high, programs will no longer run in Processing. When you hit run,
you'll get error messages.

If this message appears after you hit Run, then you're trying to use
more memory than the machine has installed:

```
Error occurred during initialization of VM
Could not reserve enough space for object heap
```

The following messages mean that you're trying to use more memory than
the Operating System allows (regardless of how much RAM you have):

```
Invalid maximum heap size: -Xmx5000m
Could not create the Java virtual machine.

Invalid maximum heap size: -Xmx5g
The specified size exceeds the maximum representable size.
Could not create the Java virtual machine.
```

On Windows with 1G of RAM, the limit seems to be in the neighborhood of
1.5GB. Mac OS X and Linux seem to allow up to just shy of 4GB, depending
on how much RAM you have installed. Usually you can allocate almost 50%
more RAM than you have installed. i.e. for a machine with 1 GB of
physical memory, about 1.5GB is the maximum that can be used. Your
mileage will also vary with different versions of Java (1.3, 1.4, 1.5,
1.6...) and your operating system.

On the other hand, Java on Windows XP, for instance, cannot address more
than 2GB properly. So with OS and JVM overhead, the total possible
memory available is in the neighborhood of 1.5GB (no matter how much RAM
you have).

Unfortunately the memory limitations of Java set an upper bound that is
outside our control. If you're having trouble creating very large images
for this reason, you might look into the PDF or DXF libraries that are
included with Processing, or the contributed Illustrator or SVG vector
export libraries that can be found on the libraries page as another
alternative for creating large format images.

Memory is like any constraint found in other media, you simply need to
be more clever about how to deal with the limitations.

To check the amount of memory that's used so far, or how much is
available, use Java's Runtime object:

```
// The amount of memory allocated so far (usually the -Xms setting)
long allocated = Runtime.getRuntime().totalMemory();

// Free memory out of the amount allocated (value above minus used)
long free = Runtime.getRuntime().freeMemory();

// The maximum amount of memory that can eventually be consumed
// by this application. This is the value set by the Preferences
// dialog box to increase the memory settings for an application.
long maximum = Runtime.getRuntime().maxMemory();
```

### Why don't these Strings equal?

Comparing a string (quoted text) is different in Processing (Java) than
it is in ActionScript or some other languages, which often confuses
people. For instance, while this might make sense:

``` {.processing}
String[] lines = loadStrings("sometext.txt");
for (int i = 0; i < lines.length; i++) {
  if (lines[i] == "hello") { 
    println("hello found on line: " + i); // you'll never see this
  }
}
```

You'll never see the message, even if "hello" is in the list. This is
because a String is an object in Java, comparing them with == will only
compare whether the two things are pointing at the same memory, not
their actual contents. Instead, use equals() or one of the other String
methods (eg. equalsIgnoreCase):

``` {.processing}
String[] lines = loadStrings("sometext.txt");
for (int i = 0; i < lines.length; i++) {
  if (lines[i].equals("hello")) {
    println("hello found on line: " + i); // happiness
  }
}
```

"*But if I write the following code, it works!*"

``` {.processing}
final String HELLO = "Hello";
String hello = "Hello";
println(hello == HELLO);
```

That's because Java compiler detects two identical constant strings, so
it groups them together, and their references (memory location) are
identical. If you write instead:

``` {.processing}
final String HELLO = "Hello";
String hell = "Hell";
println(hell + "o" == HELLO);
```

It no longer works. Same for strings coming from an external source
(file, Internet, etc.).

### Why does 2 / 5 = 0 instead of 0.4?

The result of dividing two integers will always be another integer:

``` {.processing}
int a = 2;
int b = 5;
int result = a / b;
// result is zero
```

While somewhat confusing at first, this is later useful for more
advanced programming.

To get fractions, use a 'float' instead:

``` {.processing}
float a = 2.0;
float b = 5.0;
float result = a / b;
// 'result' will be 0.4
```

It is not enough to just divide two integers and set them to a float:

``` {.processing}
 float y = 2 / 5;
```

In this case, integer 2 is divided by 5, which is zero, and then zero is
assigned to a float. The number doesn't become a float until the left
hand side of the = sign. On the other hand, this:

``` {.processing}
float y = 2.0 / 5;
```

will work just fine. In this case, Java sees that 2.0 is a float, so it
also converts the 5 to a float so that they can be divided, which makes
it identical to:

``` {.processing}
float y = 2.0 / 5.0;
```

and because floats are being used on the right hand side, the result
will be a float, even before it gets to the left hand side.

### Number Trouble (NaN and Infinity)

NaN is shorthand for "Not a number", which means the result of a
calculation is undefined. This is caused by dividing 0.0 by 0.0 or
taking the square root of a negative number. Infinity is the result of a
calculation that is too large to be normally represented by a
floating-point number. It's commonly seen as the result of dividing a
number by 0.0. Its opposite value, -Infinity, is the result of dividing
a negative number by 0.0. These unexpected results are often hidden by
variables. Check the value of your variables with print() to search for
these and similar numerical problems.

### color(0, 0, 0, 0) is Black.

The reason this doesn't work is that color(0, 0, 0, 0) creates an int
that is simply '0'. Which means that fill(color(0, 0, 0, 0)) is the same
as fill(0), which is...black. This is a problem of 'color' not being a
real type, but just an int, plus the fact that we overload fill() to use
both int/color for a color, and also an int for a gray. Since this is
unlikely to be fixed anytime soon (if ever), there are multiple
workarounds that you can use:

-   use `fill(0, 0, 0, 0)`
-   `fill(c, 0)` where `c = color(0, 0, 0)`
-   `color almostTransparent = color(0, 0, 0, 1);`
-   `color almostBlack = color(1, 1, 1, 0);`

### Key Repeat on macOS Sierra

In macOS Sierra, Apple changed how key repeat works. In most applications, when you press and hold a key for some characters, a small menu will pop up that shows possible alternates. For instance, holding `u` might pop up a menu that includes `ü` and others like it. Unfortunately, this means that pressing and holding `u` inside a Processing sketch won't work properly. To fix this, you'll have to turn off that menu, by opening Applications → Utilities → Terminal and entering: 
```
defaults write -g ApplePressAndHoldEnabled -bool false
```
You'll probably need to restart Processing after using this command.

Note that this will turn off the menu for your other applications as well, so if you need to bring back the old behavior, do the following:
```
defaults write -g ApplePressAndHoldEnabled -bool true
```

### Common Issues (That Are Not Bugs)

Things that are often perceived as bugs, but aren't actually "broken":

- Typing a semicolon after an `if()` statement and before its associated code block causes the `if` statement to do nothing: 
``` {.processing}
if (somethingAmazing == true);
{
  println("This happens, whether or not something is amazing.");
}
```
The semicolon immediately following `if ()` should *not* be present here, as it effectively closes the `if` logic, so the code block beneath it will *always* run (regardless of whether or not `somethingAmazing` is `true` or `false`).


-   If you write informal code (some test lines, no setup()) and want to
    add a function (eg. `void foo() { println("Foo"); }`) you will get
    an error: *unexpected token: void*. You need to wrap your lines of
    code (not the functions!) in setup(). Technically, that's because if
    your code has no setup() method, Processing will wrap it in a
    generated setup(). But Java doesn't allow nested methods, hence the
    error.

-   If your code has methods (it's not just in static mode) or needs to
    run over time, it must have a draw() method, otherwise nothing will
    happen. For instance, without a draw(), this code will stop after
    the setup() method:

``` {.processing}
void setup() {
  size(400, 400);
}
 
void keyPressed() {
  println(key);
}
  
```

-   An `UnsupportedClassVersionError` means that you're using code that was compiled for a later version of Java than is supported by Processing. As of the 3.0 releases, Processing supports Java 1.8. A message like `java.lang.UnsupportedClassVersionError: (Unsupported major.minor version 53.0)` means that the code was compiled for Java 1.9, which is not currently used with Processing.

-   Any code that accesses the `pixels[]` array should be placed inside
    `loadPixels()` and `updatePixels()`. This can be confusing because it
    was not required in older code, i.e. with some alpha/beta releases
    in the 1.0 series. A complete description can be found in the
    reference for the
    [pixels](http://processing.org/reference/pixels.html) array.

-   *Why doesn't saveFrame (or saveStrings or saveBytes) write things to
    the data folder?* All saveXxxx() functions use the path to the
    sketch folder, rather than its data folder. Once exported, the data
    folder will be found inside the jar file of the exported application
    or applet. In this case, it's not possible to save data into the jar
    file, because it will often be running from a server, or marked
    in-use if running from a local file system. With this in mind,
    saving to the data path doesn't make sense anyway. If you know
    you're running locally, and want to save to the data folder, use
    `saveXxxx("data/blah.dat")`.

-   Objects with alpha (lines or shapes with an alpha fill or stroke,
    images with alpha, all fonts) are displayed in P3D and OpenGL based
    on their drawing order. This creates some annoying effects like
    making things opaque if they're drawn out of order with objects
    above or beneath them. This is simply how most 3D rendering works. 
    To improve appearance, add `hint(ENABLE_DEPTH_SORT)` to `setup()`. 
    We don't enable this by default because it would make *all* sketches
    slower, not just ones that need it.

-   Names of sketches cannot start with a number, or have spaces inside.
    This is mostly because of a restriction on the naming of Java
    classes. I suppose if lots of people find this upsetting, we could
    add some extra code to unhinge the resulting class name from the
    sketch name, but it adds complexity, and complexity == bugs. :)

-   Mind the capitalization of built-in functions. If a method or
    variable name is two words, usually the first word is lowercase and
    the first letter of the second word will be capitalized. For
    instance: keyPressed, movieEvent, mouseX, etc. If you have a
    function called mousepressed(), it won't be called when mouse events
    occur, because it needs the capital P on 'pressed'.

-   On Windows, sometimes your programs will run in a window that has a
    Java coffee cup icon, instead of the usual Processing icon. This
    simply means that the application is being run outside of Processing
    as an external application. This happens when extra libraries,
    multiple source code files (more than one tab), or extra code files
    in the 'code' folder are employed.

-   To use Sound, install the Sound Library via Sketch > Add Library... > Sound. 
    The ancient `PSound` class no longer exists, and Minim 
    (the library used in 2.x) is no longer maintained and not included in Processing 3.

-   Processing sketches have a default frameRate setting of 60. 
    This prevents sketches from needlessly running too
    fast and throttling the CPU. However, this is only the "maximum"
    frame rate, if a lot of computation is in the code, the sketch will
    attempt to use as much CPU as is available. On Windows, this can
    sometimes cause audio hiccups when an MP3 player is running at the
    same time, or another application is trying to do something
    simultaneously. To fix the audio issue, add a delay(5) or delay(10)
    to your code, which will give five or ten milliseconds to other
    applications so they can breathe. For other applications, you may
    have to set the frameRate() lower, or use a longer delay().

-   If your sketch is based on Java Mode, where you explicitly say
    that the class extends PApplet, then the preprocessor assumes that
    you know what you're doing. You'll have to make sure that your code
    is named properly. This means that if you have "public class PooTime
    extends PApplet" at the beginning of your sketch, you bet your a--
    the tab will need to be named PooTime. If not, your code isn't gonna
    run. I mean, c'mon... You know what you're doing, right? This is
    also true when exporting to an application.

-   Don't name your sketch the same thing as a library or other class
    that's used in your sketch. For instance, your sketch shouldn't be
    named "Server" if you've imported the net library, because it
    already has something called Server. You can be more creative than
    that.

### Things that we probably can't fix

Some things are out of our control, or not actually bugs:

#### All Platforms

-   A long sketch menu that goes off the edge of the screen? Doesn't
    scroll properly? There's not much we can do. This is a java issue
    which happens on most platforms. To get around it, you can organize
    your sketches into subfolders which will appear as submenus (be sure
    to quit before reorganizing, and then restart when finished).

-   If you're seeing a sun.dc.pr.PRException, it's because you're trying
    to draw something that's waaaaay off screen (like an x coordinate of
    -100,000 or something nutty like that).

#### Windows

-   The system clock sometimes goes weird, especially when using
    frameRate() or delay(). This is a [long-standing
    bug](http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=4500388)
    with the Windows version of the Java VM. According to someone on the
    Sun web site: “This bug has been fixed in bug no 4500388 and one
    requires a PRODUCT FLAG to use the fix. This flag and fix are
    available in 1.3.1\_4, 1.4.0\_2, 1.4.1 and 1.4.2. But for Java to
    actually use the fix, open your Java Plug-in Control Panel in the
    section 'Java Runtime Parameters' just enter:
    -XX:+ForceTimeHighResolution”

-   Create Font sometimes crashes on Windows, bringing down the whole
    environment. This seems to be a Java bug, because it's not a Java
    exception, but a full crash.

-   Hard crashses that write `hs_err_pid10XX.txt` files are errors inside
    the Java VM, and often something that's out of our control.

#### Linux

-   The following message (or messages like it) on startup:

`Warning: Cannot convert string "-b&h-lucida-medium-r-normal-sans-*-140-*-*-p-*-iso8859-1" to type FontStruct. `

This is just a Java issue, but doesn't seem to affect anything.