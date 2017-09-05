> This document summarizes major changes in Processing through version 2.0. If you are using version 3.0, please instead reference [Changes in 3.0](https://github.com/processing/processing/wiki/Changes-in-3.0).

***

This used to work and now it doesn't
------------------------------------

The Processing Language changes as the software evolves. Some of the
most important changes are presented on this page. For each release,
read the
[revisions.txt](https://github.com/processing/processing/blob/master/build/shared/revisions.txt)
file (included with the download) to see what's changed since the
release before it. This is where you go if your code stops working in
the most recent release, or if you want to know if your favorite bug has
been fixed. If you don't want to download first, you can read the most
recent version
[here](https://github.com/processing/processing/blob/master/build/shared/revisions.txt).

Changes in Processing 2.0
-------------------------

### The Big Stuff

-   **P2D and P3D** have been replaced with variants of the OpenGL
    renderer. We've removed the software-based (but speedy for some
    circumstances) versions of P2D and P3D. We feel that OpenGL
    rendering is probably the future for most Processing work, so we're
    focusing our efforts there. The change will cause some sketches to
    actually run slower, but the bottom line is that we simply don't
    have anyone to help maintain all of this extra code. We hope to sort
    out the performance problems over time—if you see something weird,
    please report a bug.

-   **OpenGL 2** – a new version of the OpenGL library has been
    implemented, and the old one has been removed. The new library is
    based on Andres Colubri's Android work (and his experiences
    developing the GLGraphics library). All the great things from
    Android have now been back-ported to the desktop version of
    Processing, so we have a super fast OpenGL library.

-   **OpenGL is now part of core** – the OpenGL library is now built
    into the core, no need to include it as a separate library. This
    simplifies things (enormously), and brings better parity with other
    platforms like Android. This makes exported applications larger, but
    the benefits are worth it.

-   **Modes** – if you've used Processing 1.5, you'll know about the
    built-in Android mode, but if not, Processing now supports multiple
    languages and platforms. At the right-hand side of the editor window
    is a drop-down menu that allows you to choose between "Java",
    "Android", and "JavaScript" mode. Those are the current modes that
    are being included, though we may add/remove modes as we head to 2.0
    (a Jython mode is lurking about, for instance. Mmmm! Tempting.) Like
    Tools and Libraries, it will be possible for other parties to write
    their own modes that work inside the PDE.

-   **JavaScript** – the JavaScript mode (see above) allows you to write
    a sketch and quickly run it in a browser using
    [Processing.js](http://processingjs.org). The code that glues PJS to
    the PDE was developed by long-time Processing contributor Florian
    Jenett, and continues to evolve. We highly recommend using
    JavaScript for running Processing work in web browsers.

-   **Video** – we've removed the QuickTime for Java video library and
    are using a modified version of Andres Colubri's GSVideo library
    instead. On Linux, you'll need to install gstreamer to use the new
    library. On Windows and Mac OS X, you should not need to install it,
    however we're working out a few kinks in the whole process.

-   **Movie Maker** – the MovieMaker class has been removed, because it
    was specific to QuickTime for Java. In its place there is now a
    Movie Maker item under the Tools menu, that helps you convert a file
    of frames into a video file. There isn't a good library-based method
    to make this work, so it'll probably stay a Tool rather than be
    re-incorporated into the video library.

-   A new class called **XML** replaces the old `XMLElement`. With the
    change, you can call loadXML("blah.xml") from inside PApplet to read
    XML data. The rest of the API is the same as it was for XMLElement,
    except that getXxxxAttribute() is now just getXxxx(), for instance
    getIntAttribute() is just getInt() (to be more like the rest of the
    Processing API). Also added XML.parse(String) which returns an XML
    object from a String of XML data. Whitespace is preserved more
    consistently with the new implementation, which might require some
    changes to your code. To load an XML file, use the following syntax:

    `XML xml = loadXML("fancy.xml");`

    do not use:

    `XML xml = new XML("fancy.xml");`

     unless you want to do exception handling while loading. It's there for
     advanced users, but not recommended for most. The latter version is not
     supported, and not officially part of the Processing API.

-   A new **Table** class has been added, making it easy to deal with
    comma- or tab-delimited data files such as a spreadsheet. More on
    this later.

-   Java **Applet** support is being removed, starting in 2.0 alpha 7.
    It simply doesn't make sense to support these anymore, given our
    priorities, lack of web browser support, and I don't have any time
    to support them. A steady parade of issues like [this
    one](http://code.google.com/p/processing/issues/detail?id=775),
    while browser makers and OS vendors make applets all the more
    difficult and unappealing is a losing battle and life is too short
    for such things. It's an unfortunate change, but simply the reality
    of where we're at. Applets were always an important, essential part
    of Processing because it was important to be able to make your work
    available online. At the moment, using Processing JS (or Processing
    1.5) is instead generally a better option for things that run on the
    web. (And before anyone asks, no, we will not be adding JNLP support
    in its place. If someone wants that, they should write a JNLP Export
    Tool.)

-   Better **32 and 64-bit support**. We now support separate 32- and
    64-bit libraries and have added separate 32- and 64-bit versions of
    the Processing download. On Mac OS X, you can even select which mode
    you'd like to use. On Windows and Linux, you'll just have to use the
    32- or 64-bit download to run in that mode. Using 32-bit on a 64-bit
    Linux machine may require installation of some compatibility
    libraries for your distribution.

- Removed all imports that aren't covered in the Processing reference. 
  If you use java.awt, java.util, or other classes in your sketch, you
  will need to add an import line to the beginning of your sketch.

  Only the classes that are covered in the reference (HashMap, ArrayList, 
  and some others) are now imported by default. This has been done to improve
  overall cross-platform parity and to avoid users unknowingly adding 
  Java classes, and then the sadness that comes when switching to Android
  or JavaScript modes. 

  The list of imports is now hard-coded (no longer read from preferences.txt)
  and includes the following:
  ```
  import java.util.HashMap;
  import java.util.ArrayList;
  import java.io.BufferedReader;
  import java.io.File;
  import java.io.PrintWriter;
  import java.io.InputStream;
  import java.io.OutputStream;
  import java.io.IOException;
  ```

  If we're missing anything that's covered in the reference, please let us 
  know via the bugs database.

### Drawing Quality

**Lines and strokes sometimes uglier** – When using the default
renderer, a stroke() on a shape may be uglier than in the past, due to
recent changes that Oracle has made to Java. Usually this is a problem
with single pixel strokes and rough edges, or thick strokes with many
steps. To fix the problem, add hint(ENABLE\_STROKE\_PURE) to the setup()
block of your sketch. We don't enable it by default because it makes all
sketches considerably slower.

**2D drawing with OpenGL** – When drawing 2D objects with OpenGL, use
P2D as the renderer (instead of P3D). There are several tradeoffs in
rendering 2D versus 3D, so two-dimensional drawing inside P3D will
generally be of unacceptable quality for 2D.

### Event Handling

Event Handling has changed significantly in 2.0b7. Due to necessary
changes in the OpenGL renderer, and to provide better compatibility with
Android and JavaScript modes, we've added actual MouseEvent and KeyEvent
classes to Processing. In previous releases, the MouseEvent and KeyEvent
classes referred to the automatically imported "java.awt.MouseEvent" and
"java.awt.KeyEvent". This is no longer the case, so your code will
behave a little differently. The OpenGL renderer no longer uses AWT (and
therefore doesn't use java.awt events), so it's a necessary change
there. On Android, there's no such thing as java.awt. More details on
this as I have time to write them up.

This also has implications for libraries, and the [library developer
pages](https://github.com/processing/processing/wiki/Library-Basics)
have more information.

### Added and Improved

-   Added **rounded rectangles** via rect(x, y, w, h, radius) and
    rect(x, y, w, h, tl, tr, br, bl).

-   If you try to run more than one copy of Processing at a time, it
    will steadfastly refuse (and simply quit again). Instead of just 
    quitting the application, it will bring the already running 
    Processing app to the front, and if you were opening a file,
    it will open that sketch.

-   It's possible to control which display is used when running or
    presenting a sketch. You can find the option in the Preferences
    dialog box.

### Changed and Removed

-   **screen.width** and **screen.height** have been replaced by
    `displayWidth` and `displayHeight` (in 2.0a6). The originals were
    only half-documented and didn't properly fit with the rest of the
    Processing syntax. Prior to 2.0a6 `screenWidth` and `screenHeight`
    were used instead of `displayWidth` and `displayHeight`, however
    those aren't a good name when dealing with multiple display setups,
    for which we may be adding a `displayX` and `displayY` variable (not
    all displays start at 0,0). That would conflict with the
    already-existing `screenX/Y/Z` methods, for which `screenWidth()`
    and `screenHeight()` methods may be added down the road for
    measuring on-screen size of objects.

-   ~~**delay()** has been removed. Nobody understood what it did, and
    when they did, they didn't understand why it was there. Huge source
    of confusion, especially for beginning students.~~ Ugh, **delay()**
    is back in 2.0a5. Not having it there is an annoyance for scripting
    and serial apps.

-   **textMode(SCREEN)** has been removed. SCREEN was a super
    fast/efficient way of rendering text with P2D and P3D, but since
    they're going bye-bye and it's actually slower in the remaining
    renderers, it's going away.

-   **registerSize()** has been removed for libraries. It hasn't worked
    for a long time, now it's just removed. This isn't a good way to get
    the current size anyway, because resize events don't go through the
    size() command. Just check the width and height inside another
    library method (**pre()** or **draw()** for instance) instead.

-   **text(x, y, w, h, z)** (text in a rectangle with a z-coordinate)
    was removed, due to its general inconsistency in syntax, lack of
    use, and the fact that its implementation contains nothing useful
    outside of calling **translate()** for you.

-   **text()** with no x- or y-coordinate has been removed. While useful
    to continue lines of text without keeping track of text width, this
    was never documented, inconsistent with other API (3D in particular,
    where no x, y coordinate would be assumed to mean (0, 0) like
    **sphere()** or **box()**). With this, the textX, textY, and textZ
    inside PGraphics have also been removed.

-   Long unused constants **CENTER\_RADIUS**, **CENTER\_DIAMETER**,
    **NORMALIZED** have been removed.

-   The `online` boolean has been deprecated. The reason is that it has
    nothing to do with whether a sketch is online (i.e. had a net
    connection), but rather it would return true if the sketch was
    running inside a web browser or applet viewer. (Technical version:
    whether a Java AppletContext existed.)

-   **selectInput()**, **selectOutput()**, and **selectFolder()** have
    all been modified. The old versions have been removed because it
    wasn't actually possible to fix them. The new versions use a
    callback scheme, meaning that you provide the name of a function
    that will be called after a file has been selected. This is because
    the file chooser window must operate in a separate thread from the
    rest of your sketch. The new methods are:

```
void selectInput(String prompt, String callback);
void selectInput(String prompt, String callback, File file);
void selectInput(String prompt, String callback, File file, Object callbackObject);
```

An example of using `selectInput` is below.

```
void setup() {
  selectInput("Select a file to process:", "fileSelected");
}

void fileSelected(File selection) {
  if (selection == null) {
    println("Window was closed or the user hit cancel.");
  } else {
    println("User selected " + selection.getAbsolutePath());
  }
}
```
Passing in a File object will provide a default file to be used. Passing
in a callbackObject allows you to call a method in a class other than
your primary sketch.

### OpenGL Changes

-   The new version of the OpenGL library requires drivers that support
    OpenGL 2.0. This allows us to keep OpenGL support for desktop and
    Android in sync with one another. Unfortunately this means that some
    older cards and drivers (particularly on Linux) will not work, and
    that Processing 2.0 on such machines will be limited to 2D graphics.
    But the OpenGL library is developed by a single person (Andres
    Colubri), who works on this in his free time, and he can't support
    two separate video libraries with radically different
    implementations. Keep in mind you can always use Processing 1.5.1 to
    continue 3D development, though it will not be updated further, and
    we won't be accepting bug reports for it.

-   There was a bug in the lighting attenuation factor that was fixed in
    2.0a5. This will mean that some lighting will look a little bit
    different.

-   We'll only be supporting Android 2.3.3 (Gingerbread, API 10) and
    later, starting with Processing 2.0a5. Due to a [major API
    omission](http://code.google.com/p/android/issues/detail?id=8931) in
    the OpenGL bindings before 2.3.3, we can't support the earlier OS.
    There could be ways around this, or we could require 2.3 only when
    using OpenGL, but we don't have enough (any) developers to support
    this sort of thing.

-   OpenGL sketches on Mac OS X will print an error message upon
    starting (or when changing the smooth level with
    *smooth()*/*noSmooth()*) that looks like: *2012-03-27 16:25:12.317
    java[5741:1707] invalid drawable*. This is [an issue with Apple's
    Java plugin](http://lwjgl.org/forum/index.php?topic=4460.new) which
    seems to have no effect.

-   Calling *smooth()* and *noSmooth()* causes the OpenGL drawing
    surface to be recreated. Don't do that. Call one inside *setup()*
    and stick with it. Otherwise you'll get lots of flickering as it's
    rebuilt on each frame.

### Known Issues and What's Coming

-   createShape() has not been implemented for the default 2D renderer.
    (issue 1400)

-   A better interface for **installing and updating libraries, tools,
    and modes**. Our Google Summer of Code project will be getting more
    refined over time.

Changes in Processing 1.0 (revision 0162)
-----------------------------------------

The biggest changes in the months prior to release 1.0 are as follows:

-   **Libraries** - All libraries must be placed in a folder named
    "libraries", inside the sketchbook folder. Do not use the main
    "libraries" directory in the Processing distribution, as it is
    reserved for the core libraries, and is not visible on Mac OS X.

-   **XML** - The XML library is now included by default, so you won't
    find it in the Import Library menu anymore. In addition, the XML
    library since 0135 has been greatly improved, making it compatible
    with far more documents.

-   **Processing.app** - The Mac OS X release of Processing is now a
    single .app file, more befitting an OS X application.

-   **Processing.exe** - The Windows release has a new launcher based on
    [launch4j](http://launch4j.sourceforge.net/). Unfortunately, some
    machines [have a
    problem](http://dev.processing.org/bugs/show_bug.cgi?id=986) with
    the new launcher that we haven't been able to track down. If you
    have trouble, please [help us find the
    problem](http://dev.processing.org/bugs/show_bug.cgi?id=986). PDE
    files are also now double-clickable on Windows.

-   **OpenGL** - All OpenGL sketches now use 2x full screen
    anti-aliasing. This means that these sketches are always smooth, and
    the smooth() and noSmooth() commands are ignored. To return to the
    behavior found in the beta releases, see the
    [hint()](http://processing.org/reference/hint_.html) reference.

-   **P2D and P3D** - The P2D renderer has returned (see the
    [size()](http://processing.org/reference/size_.html) reference) and
    smoothing is now enabled for both P2D and P3D. Smoothing support is
    unfortunately incomplete, however, and sometimes thin lines can be
    seen inside shapes. This is a very high priority
    [bug](http://dev.processing.org/bugs/show_bug.cgi?id=200) to be
    fixed in a future release.

-   **Candy and PShape** - The Candy SVG library has been merged into
    the core, which brings along a new
    [loadShape()](http://processing.org/reference/loadShape_.html)
    function and a new
    [PShape](http://processing.org/reference/PShape.html) object. The
    special powers of PShape will be rolled out in future releases. For
    the time being, loadShape() works best with the default renderer
    (JAVA2D). Complex shapes will often appear jagged or not at all when
    rendered with [P2D,
    P3D](http://dev.processing.org/bugs/show_bug.cgi?id=1053), and
    [OPENGL](http://dev.processing.org/bugs/show_bug.cgi?id=947). We've
    also added better support for SVG files created with Inkscape.

-   **PVector** - We've added a new class called
    [PVector](http://processing.org/reference/PVector.html), which is a
    simple three-dimensional vector (also known as point or tuple)
    class. This is useful for storing point data, or operations on 3D
    points.

-   **Tools** - A new Tools API has been created for developers who want
    to contribute code that extends the Processing Development
    Environment in some fashion. Let your creativity flow with
    fantastical contributions like "Color Selector 2.0", "ROT13 Code
    Mangler", and "I Am Rich". Visit the [developer
    page](https://github.com/processing/processing/wiki/Tool-Overview)
    on tools for more information. Similar to libraries, tools are
    installed in a folder of the same name within your sketchbook
    folder.

-   **Asynchronous Images** - Big JPEGs and small pipes? We've added a
    new
    [requestImage()](http://processing.org/reference/requestImage_.html)
    method that loads an image in the background so that your sketch
    doesn't freeze when loading lots of large images over a slow
    connection.

-   **Sound** - We've added Damien Di Fede's
    [Minim](http://code.compartmental.net/tools/minim/) library to the
    download. It uses the JavaSound API to provide an easy-to-use audio
    library. Minim has a simple API while still providing a reasonable
    amount of flexibility for more advanced users. Many thanks for
    Damien for his hard work on this excellent library.

-   **Present** - Present mode (full screen) is handled differently in
    1.0. When run inside the PDE, only Mac OS X uses full “screen
    exclusive mode” with Present. Windows and Linux just do full screen
    windows. When run outside the PDE, all three simply create an
    undecorated window the size of the entire screen, and on the Mac, an
    option is added to the Info.plist file to hide the dock and menubar
    (since that cannot be done programatically from inside Java
    applications).

-   **Compiler** - We've removed the old Jikes compiler and are now
    using the ECJ compiler from the Eclipse project. We've also tried
    hard to improve the quality of error messages, though some are still
    real gems that sound like error messages from mainframe computers in
    1970s films. If you don't like the messages [please help us improve
    them](https://github.com/processing/processing).

-   **Internationalization** - For better internationalization support,
    we've changed to UTF-8 encoding when loading and saving sketches.
    Sketches that contain non-ASCII characters and were saved with
    Processing 0140 and earlier may look strange when opened. Garbled
    text and odd characters may appear where umlauts, cedillas, and
    Japanese formerly lived. If this happens, use the "Fix Encoding &
    Reload" option under the Tools menu. This will reload your sketch
    using the same method as previous versions of Processing, at which
    point you can re-save it which will write a proper UTF-8 version.

-   **Java** - Linux and Windows now inlude Java 6 update 10 with the
    download. We still [don't have
    support](http://dev.processing.org/bugs/show_bug.cgi?id=598) for
    Java 1.5 syntax yet, but we hope that the performance boosts in Java
    6 will help applications run well.

Under the old numbering system, Processing 1.0 is revision 0162.

Changes in Beta 0116+ (approaching 1.0)
---------------------------------------

Release 0116 contains many changes, frameRate(), beginShape(), and
endShape() are the biggest ones.

-   framerate() is now called frameRate(), for better API consistency.
    It didn't make sense to have a frameCount variable and a framerate()
    method as its misshapen cousin.

-   The default frame rate is now 60 fps. This will prevent some odd
    quirks with sketches running faster than they need to and throttling
    the resources of your machine. To disable this, you can set the
    frame rate arbitrarily high.

-   beginShape() has changed. LINE\_LOOP and LINE\_STRIP have been
    removed because they are redundant, and not consistent with the rest
    of the API. beginShape(POLYGON) is no longer recommended, simply use
    beginShape() with no parameters when drawing an irregular shape.
    Code examples:

``` {.processing}
//OLD SYNTAX:
beginShape(POLYGON);
// call vertex() several times
endShape()

//NEW SYNTAX:
beginShape();
// call vertex() several times
endShape(CLOSE);
```

endShape() with the CLOSE parameter will make the stroke on your shape
continue back to where the shape started. This is the same way that
POLYGON and LINE\_LOOP worked.

``` {.processing}
//OLD_SYNTAX:
beginShape(LINE_STRIP);
// draw with vertex()
endShape();
  
// NEW SYNTAX:
noFill();
beginShape();
// draw with vertex();
endShape();
```

In the above case, noFill() must be called, and the CLOSE parameter to
endShape() is not used, because the last point should not come back to
meet the original point.

``` {.processing}
// OLD SYNTAX:
beginShape(LINE_LOOP);
// draw with vertex()
endShape();

// NEW SYNTAX:
noFill();
beginShape();
// draw with vertex();
endShape(CLOSE);
```

For the LINE\_LOOP example, endShape(CLOSE) is used to specify close the
shape. noFill() must also be called, so that the shape is not filled in.
The two main problems with the old API were 1) LINE\_LOOP was simply a
POLYGON with no fill setting, this made for a strange inconsistency. 2)
there was no way to draw a non-closed POLYGON shape. Using
beginShape(POLYGON) doesn't make much sense when you're drawing a line,
so this is one more reason that beginShape() with no parameters is
recommended.

-   The single pixel blend() methods have been removed, they were
    overkill. Also, the blend() function that blends a color, instead of
    image data, is now called blendColor().

-   Along with blendColor(), a lerpColor() method has been added. It
    works just like lerp()... but with colors!

-   writer() and reader() are now createWriter() and createReader().

-   toInt() and toFloat() are now parseInt() and parseFloat(), to change
    to JavaScript syntax. Not sure if anyone was using these.

-   Text with the JAVA2D setting no longer uses native fonts by default,
    which means they'll be slower and uglier. See the reference for
    [textFont()](http://processing.org/reference/textFont_.html) for
    details and how it can be addressed.

-   Threading has been modified signficantly. Some of these changes had
    to be undone at the last minute, so further changes are coming. The
    changes will fix several strange InterruptedException problems.

-   The PGraphics classes have all been reworked and renamed.
    -   PGraphics is an abstract class on which additional PGraphics
        subclasses can be built. It is an abstract class, and therefore
        cannot be invoked directly.
    -   PGraphics2D (P2D) contains the former contents of PGraphics that
        are specific to 2D rendering. This will be P2D once it is
        complete. As of release 0126, P2D is not currently complete and
        cannot be used.
    -   PGraphics3D (P3D), formerly PGraphics3, remains mostly
        unchanged.
    -   PGraphicsJava2D (JAVA2D), formerly PGraphics2, is the renderer
        used when you call size(w, h) or size(w, h, JAVA2D). It remains
        the default renderer when none is specified. It is slower but
        more accurate than the others.
    -   PGraphicsOpenGL (OPENGL) is the new name for PGraphicsGL.

-   Do not use "new PGraphics" to create PGraphics objects. Instead, use
    [createGraphics()](http://processing.org/reference/createGraphics_.html),
    which will properly handle connecting the new graphics object to its
    parent sketch, and will enable save() to work properly. See the
    reference for createGraphics.

-   For the same reasons as above, createImage(width, height, format)
    should be used instead of "new PImage" when [creating
    images](http://processing.org/reference/createImage_.html).

-   More recent releases include better support for ARGB format images.
    This is helpful for using createImage() or createGraphics() to
    generate a transparent surface. Be sure to use PNG or another format
    that supports alpha. This support is incomplete, however, and there
    are a handful of bugs.

-   beginFrame() and endFrame() are now beginDraw() and endDraw(). Use
    these around drawing commands to a PGraphics created by
    createGraphics(). The defaults() method should not/need not be
    called, just beginDraw() and endDraw().

Changes between Alpha (Release 0069) and Beta (Release 0085)
------------------------------------------------------------

Between revision 0069 (the last public alpha) and the beta release
(0085), many, many functions have been added, and are detailed in the
[reference](http://processing.org/reference/). Aside from that, this
page lists functions whose names have changed or fundamental API
differences between the two versions.

-   loop() has been removed, and is instead called draw(). If you want
    applications to only run draw() once (the way draw() used to work),
    use the function noLoop() inside of setup().

-   size() should now be the very first thing in your setup(), otherwise
    commands that come before it may be ignored. your settings for
    fill() and stroke(), for instance, will disappear after you call
    size().

-   2D and 3D graphics are no longer completely mixed. To specify 3D
    graphics, instead of size(200, 200), the new way is to use size(200,
    200, P3D).

-   You may find that by default, your code runs more slowly in a beta
    release than an alpha release. The new renderers might be slower for
    some things, faster for others. If you want faster pixel operations,
    try using P3D (until P2D is available). For high-quality lines and
    strokeWeight() and strokeCap(), use JAVA2D (the default).

-   BImage → PImage, BFont → PFont, and so on...

-   For advanced users who were making their own BGraphics objects in
    the previous release:

``` {.processing}
BGraphics bg = new BGraphics(200, 200);
```

should be changed to:

``` {.processing}
 PGraphics pg = createGraphics(200, 200);
 pg.beginDraw();
 // drawing commands for pg here
 pg.endDraw();
```

~~We didn't realize quite how many people were using this, so we'll
probably add a createGraphics() method because PGraphics2 may be
temporary (instead of just PGraphics), and the "null" thing is pretty
weird. Even still, this isn't quite working as expected, but it's a high
priority to fix for the future, see Bug 92 for the status.~~

-   To use OpenGL rendering, change that to size(200, 200, OPENGL), and
    use Sketch → Import Library → opengl. OpenGL support is incomplete,
    but allows for much larger screen sizes and accelerated graphics
    that make use of a decent graphics card.

-   When using the pixels[] array of the main window, or on an image,
    you should first call loadPixels(). Once you're done editing, call
    updatePixels(). This is because the new JAVA2D and OPENGL renderers
    both need to post-process the image data before displaying it, which
    is a time-consuming operation.

-   Library events are handled differently because more than one serial
    port or video input device can be used with Processing beta. See the
    documentation for movieEvent(), captureEvent(), and serialEvent().

-   push() → pushMatrix()

-   pop() → popMatrix()

-   textureMode(NORMAL\_SPACE) → textureMode(NORMALIZED)

-   textureMode(IMAGE\_SPACE) → textureMode(IMAGE)

-   textMode(ALIGN\_LEFT) → textAlign(LEFT)

-   textMode(ALIGN\_RIGHT) → textAlign(RIGHT)

-   textMode(ALIGN\_CENTER) → textAlign(CENTER)

-   textSpace(SCREEN\_SPACE) → textMode(SCREEN)

-   textSpace(OBJECT\_SPACE) → textMode(MODEL)

-   font.width(String s) → textWidth(String s)

-   font.ascent() → textAscent()

-   font.descent() → textDescent()

-   Fonts should now be more accurately sized, if your font sizing looks
    weird, try using "Create Font" to create a new font using the most
    recent release of Processing. It's strongly suggested that you do
    this when updated projects from alpha to beta.

-   The function alpha(), when used to create an alpha mask of an image,
    is now [mask()](http://processing.org/reference/PImage_mask_.html),
    to remove a conflict with the alpha() function that extracts the
    alpha value of a color.

-   Previous default ellipseMode was CORNER → now it's
    ellipseMode(CENTER)

-   RGBA for images → ARGB (more technically accurate)

-   CENTER\_DIAMETER → CENTER

-   objectX, objectY, objectZ → modelX, modelY, modelZ

-   curveSegments() → curveDetail()

-   bezierSegments() → bezierDetail()

-   splitStrings() → split() (changed in rev 0069)

-   splitInts() → toInt(split()) (changed in rev 0069)

-   splitFloats() → toFloat(split()) (changed in rev 0069)

-   angleMode() has been removed. Radians are used for all functions. If
    you don't like radians, you can convert to radians to degrees via
    the radians() function, i.e.: sin(radians(90)).

-   Four calls to bezierVertex(x, y) should instead be a single call to
    vertex(x, y), followed by bezierVertex(cx1, cy1, cx2, cy2, x2, y2)
    (two control points followed by the destination point).

-   The libraries for serial, video, and network have changed
    completely. Check out the examples or visit the [libraries
    reference](http://processing.org/reference/libraries/) for the full
    details.