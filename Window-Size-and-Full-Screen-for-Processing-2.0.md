> This page is for Processing 2, and covers things that have vastly improved in Processing 3. If you're interested in this information, use Processing 3 instead! 
> This page will be updated someday when we have a moment.

---

This page covers window sizing with sketches as well as Present (full
screen) mode. In Processing 2.0 (starting with alpha 6), there are
several improvements and changes to how full screen is handled, as well
as much-improved multiple monitor support.

Making Sketches Resizable
-------------------------

This section only pertains to the desktop version of Processing (not
JavaScript or Android), because it's the only one to use windows and
frames.

It's possible to make the sketch window resizable. To do this, use the
following:

``` {.Processing}
void setup() {
  size(400, 400);  // size always goes first!
  if (frame != null) {
    frame.setResizable(true);
  }
}
```

This is not enabled by default because most sketches won't behave well
when resized. If a sketch is running inside a web browser, the `frame`
variable will be null.

You can also change the size of the window using the Java method
`frame.setSize(w, h)`. Note that you must first set the frame to be
resizable.

Running at Full Screen
----------------------

Just use Sketch → Present and your sketch will run in Full Screen mode.

#### The displayWidth and displayHeight variables

The `displayWidth` and `displayHeight` variables contain the width and
height of the screen where the sketch was launched. So to run a sketch
that uses the full width and height of the screen, use the following:

``` {.Processing}
void setup() {
  size(displayWidth, displayHeight);
}
```

You'll still need to use Present to start the sketch, otherwise the
window will have a frame around it, unless you use `sketchFullScreen()`,
described below.

Note that if you move the sketch to another display while it's running,
these variables will not update.

In Processing 1.x, an undocumented feature was the presence of
`screen.width` and `screen.height`. We didn't handle these properly, and
they don't fit with the rest of the API (plus they use a class that's
not available on Android) so we've removed them.

In Ubuntu Linux under Unity, the default desktop environment, it's often 
not possible to cover the screen completely with your Processing sketch.
You can use a second [desktop environment](http://askubuntu.com/questions/65083/what-kinds-of-desktop-environments-and-shells-are-available) which does full screen just fine.

#### The sketchFullScreen() method

Adding this method to your code will automatically start your sketch in
full screen mode, without having to use Sketch → Present.

``` {.Processing}
boolean sketchFullScreen() {
  return true;
}
```

By using this mode, Processing doesn't have to guess whether you're
going to run full screen, which can simplify things a little.

#### Full Screen Exclusive Mode

Full Screen Exclusive Mode (FSEM) has been removed in 2.0. It was prone
to causing bugs and we instead added code (from Hansi Raber, thank you!)
to hide the menu bar on Mac OS X so that full screen could be achieved
without FSEM. 

#### Disabling Full Screen Mode

You can use the Java method `frame.setSize(w, h)` to change the size of
the window, even one that has started at full screen. However, this
window will not have a title bar. It's just too problematic and prone to
bugs to toggle between the two types of windows (full screen with no
extra edges, and a smaller window with title bar and grow box). I have
enough nights that I wake up thinking about Processing bugs that I don't
need to add these to my list.

Using Multiple Monitors
-----------------------

A lot of effort has gone into fixing up support for multiple displays in
2.0.

By default, a full screen application doesn't cover multiple displays.
This is often the preferred solution (for instance, when coding on one
monitor and displaying on another). In some cases (usually involving
OpenGL), using a single sketch across multiple displays may cause it to
run more slowly. This depends on the graphics card, drivers, etc. and is
out of our control.

#### “Run sketches on display” option in Preferences

A new option has been added to the Preferences window that sets the
display where sketches are initially placed. As usual, if the sketch
window is moved, it will re-open at the same location, however when
running in Present (full screen) mode, the display selected here will
always be used.

When exporting an application, that display preference will be saved
into the exported application.

For the technically inclined, this is implemented by using the
`--full-screen` and `--display=N` command line parameters for
[PApplet](http://processing.googlecode.com/svn/trunk/processing/build/javadoc/core/processing/core/PApplet.html).

#### Running a sketch across multiple displays

If you want Present to to use multiple monitors set your size() command
to specify the full width and height of the available displays. This can
be tricky because multiple displays are often different sizes, or their
positions have negative values. There isn't a good way for us to
implement this automatically, because there are an infinite number of
ways that it can go wrong (which would lead to a similarly infinite
stream of bug reports).

#### sketchWidth() and sketchHeight() methods

Similar to what's happening on [Android](Android "wikilink"), it's often
better to simply add methods to your sketch that return the sketch width
and height. This is the most error-free way to set up a sketch. So for a
sketch that reads:

``` {.processing}
  void setup() {
    size(displayWidth, displayHeight, P3D);
  }
  
```

That can instead be written as:

``` {.processing}
  void setup() {
  }

  public int sketchWidth() {
    return displayWidth;
  }

  public int sketchHeight() {
    return displayHeight;
  }

  public String sketchRenderer() {
    return P3D; 
  }
  
```

This helps to avoid the behind-the-scenes magic of restarting the sketch
when the renderer is changed, for instance.

We don't require these methods on the desktop version of Processing
(yet) because it's tedious, however we may in the future for those using
Eclipse or other environments (inside the PDE, the size() command will
automatically add them).