> This document summarizes major changes in Processing between versions 2.0 and 3.0. If you are updating code from 1.x to 2.x, use [this page](https://github.com/processing/processing/wiki/Changes).


Changes in Processing 3.0
-------------------------

This page lists the most important changes between Processing 3 for people who are familiar with Processing 2. For more specific details, read the [revisions.txt](https://github.com/processing/processing/blob/master/build/shared/revisions.txt) file to see what's changed since the release before it. This is where you go if your code stops working in the most recent release, or if you want to know if your favorite bug has been fixed. 

### The Big Stuff

- **Rendering rebuilt** - OpenGL (`P2D` and `P3D`) is now stutter-free and very speedy. Some `JAVA2D` performance improvements as well. The new `FX2D` renderer offers huge speedups for 2D drawing, especially with high density “retina” displays.

- **New editor** — The main editor window now includes:
   - Autocomplete! (can be activated in Preferences)
   - A full-featured, easy to use debugger
   - [Tweak Mode](http://galsasson.com/tweakmode/) has been incorporated

- **New interface** - the UI has received a major makeover.

- **High-res display support** — New methods `pixelDensity()` and `displayDensity()` make it easier to create sketches that will run nicely on high-res ("Retina") displays. It sounds so simple when put that way, but this is a really big deal.

- **Unified Contributions Manager** — We used to have separate windows for installing Libraries, Modes, and Tools. Now a single "Contributions Manager" helps you manage installation and updates for all of these contributions by third-party authors, plus... Examples!

- **Sketchbook Migration** — If you already have a (2.x) sketchbook, 3.0 will ask if you want to create a new, 3.0-specific sketchbook, or share the existing one.



### Things That May Break Your 2.x Sketches

- **Do not use variables in `size()`** - This time we really mean it. We've been saying that `size()` must be the first line in setup [since at least 2004](https://web.archive.org/web/20040415021218/http://processing.org/reference/size_.html), and that using variables instead of numbers will cause problems [since 2006](https://web.archive.org/web/20060108200811/http://processing.org/reference/size_.html), and by at least 2009, simply "don't do it", but now the chickens have come home to roost. In the past, the `size()` function was implemented by doing backflips behind the scenes. Those backflips made things very fragile, introduced cross-platform quirks that have consumed too many of my weekends, and prevented us from making wholesale performance improvements to the rendering system (higher performance, better full screen support, etc). **But despair not!** If you must change the size of your sketch, use `surface.setSize(w, h)` which is the one and only (safe) way to alter your sketch's size. A short demo that's both resizable *and* gives you a random sketch window size whenever you hit a key:
``` {.processing}
void setup() {
  size(400, 400);
  surface.setResizable(true);
}

void draw() {
  background(255);
  line(100, 100, width-100, height-100);
}

void keyPressed() {
  surface.setSize(round(random(200, 500)), round(random(200, 500)));
}
```

- **Applet is gone** — Java's `java.awt.Applet` is no longer the base class used by `PApplet`, so any sketches that make use of Applet-specific methods (or assume that a `PApplet` is a Java AWT `Component` object) will need to be rewritten.

- **You only smooth once** — `smooth()` and `noSmooth()` can only be used in `setup()`, and only once per sketch. Note that `smooth()` has enabled by default since 2.x, so it's unlikely you'll need it anyway.

For the curious or insomniac, [this document](https://github.com/processing/processing/blob/master/core/README.md) has the technical details about why these changes were made.


### New

- Use the `FX2D` renderer for greatly improved 2D graphics performance. It has many improvements over the default renderer, though it has a few rough edges so we haven't made it the default. 

- `fullScreen()` method makes it much easier to run sketches in, well, full-screen mode.

- The `PVector` class now supports chaining methods.

- SVG Export that works just like the PDF Export

- A new `settings()` method that is called behind the scenes. Most users will never notice this, but if you're using Processing without its preprocessor (i.e. from Eclipse or a similar development environment), then put any calls to `size()`, `fullScreen()`, `smooth()`, `noSmooth()`, and `pixelDensity()` into that method. More information can be found in [the reference](https://processing.org/reference/settings_.html). *Only users who are in other development environments should use `settings()`.* It shouldn't be used for any other purpose.

- Updated application icons.



### Changed

- The Video and Sound libraries are no longer included in the download (because they've grown too large) and must be installed separately. Use Sketch → Import Library → Add Library... to install either one. 

### Deprecated

- The variables `displayWidth` and `displayHeight` should not be used. They're still available in 3.0 so that less code breaks in the meantime, but that won't last forever.

### Removed

- Lots of bugs


### Known Issues

- There are [plenty of issues](https://github.com/processing/processing/issues) and we could use some help!
- On Windows, launch4j [doesn't work](https://github.com/processing/processing/issues/3543) from folders with non-native charsets. On an English version of a Windows system, any characters in CP1252 are fine. 
- When using `cursor()` in P2D and P3D, the [cursor images](https://github.com/processing/processing/issues/3791) do not match what you expect from the OS. 
- When using `selectInput()`, `selectOutput()`, and `selectFolder()` with OpenGL on Windows, the [sketch window will close](https://github.com/processing/processing/issues/3831) until the file is selected. We're waiting for an upstream fix from the JOGL project. 
- It's not really a 3.0 change, but Apple changed how key repeat works in macOS Sierra, which will break some projects. See [here](https://github.com/processing/processing/wiki/Troubleshooting#key-repeat-on-macos-sierra) for details and how to fix it.

***

### Changes for Libraries, Modes, and Tools 

Some Libraries, and *all* Modes and Tools will need to be updated to be compatible with 3.0. If you've written one of these, thank you! and read on:

- For the vast majority of authors, the changes are quite simple, and involve class name or package changes inside `processing.app`. 
  - The exception is any Library where 1) assumptions were made about `PApplet` being a subclass of `Applet` (and `Component`), or 2) relied on AWT-specific features in `processing.core`. More about the changes to core can be found [here](https://github.com/processing/processing/tree/master/core).

- Modes and Tools need slight modifications because much of the UI code for Processing has moved from the `processing.app` package (which had grown unmanageably large) into `processing.app.ui`. This doesn't give us the perfect separate of UI and non-UI code that CS professors dream about, but it's a helpful step in the right direction. 

- Several of the (static) utility functions from `Base` have moved into classes called `Util`, `Messages`, and `Platform` because `Base` was getting enormous. (It still is enormous, but it's now a wee bit more reasonable.) Since enough other things are breaking in 3.0, we're not including accessors for the deprecated version of the functions, just making a clean break. Common changes will include:
  - `Base.isMacOS()` or `Base.isWindows()` becomes `Platform.isMacOS()` and `Platform.isWindows()` (sensible, right?)
  - `Base.showWarning()` becomes `Messages.showWarning()`
  - `Base.log()` becomes `Messages.log()`
  - A good rule of thumb is that if there are platform-specific qualities to it, it's probably in `Platform`. If it's a message (whether a dialog box or a log file), it's probably in `Messages`. And all those file utilities are in that `Util` class.

- Modes (and some Tools) will also need to be updated based on the major UI changes in 3.0. The default “Java” Mode is now completely separate from the rest of the code, so it's a decent model for understanding how to use the new `EditorButton` classes and similar. If your Mode subclasses `JavaMode`, you'll want to check out how [Android Mode](https://github.com/processing/processing-android) does this and how it imports the necessary classes from the Java Mode, since they're no longer on the default `CLASSPATH`.

- Each Tool is only initialized once (in 2.x, this happened repeatedly). This saves lots of time and memory. The `init()` method was changed to pass a `Base` object instead of `Editor`, because it's necessary to call `Base.getActiveEditor()` whenever a Tool's `run()` method is called. See the [Tool Basics](https://github.com/processing/processing/wiki/Tool-Basics) page for an example.

- The 2.0 and 3.0 lists of Libraries, Modes, and Tools are stored separately, so it's possible to maintain both versions, if you'd like to do so. (Though it should be noted that all active efforts are on 3.x) Users also have the ability to use separate sketchbooks for 2.x and 3.x versions of Processing, so they can have separate versions installed while the transition happens. 

- Library authors, now is the time to reduce your reliance on AWT! In 3.0, we've moved away from AWT in a big way ([here's why](https://github.com/processing/processing/tree/master/core)). Any library features that require AWT should be treated with suspicion. Modes and Tools can still use AWT, but the OpenGL renderers (`P2D` and `P3D`) and the upcoming `FX2D` renderer don't use AWT at all. 
  - This is one reason we built the `processing.event` classes in 2.x, and have been removing spurious AWT usage from the core API, documentation, and examples.) It's now been a couple years since we made those changes.
  - The other reason is that we can't rely on AWT features when targeting JavaScript or Android, so it was encouraging bad habits.