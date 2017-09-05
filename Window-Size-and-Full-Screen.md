This page covers window sizing with sketches as well as full
screen mode. In Processing 3, there are many improvements and changes 
to how full screen is handled, as well as improved multiple monitor 
support.

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
  surface.setResizable(true);
}
```

This is not enabled by default because most sketches won't behave well when resized. 

You can also change the size of the window using the method `surface.setSize(w, h)`. Note that you must first set the frame to be resizable. The size change is not instantaneous, however—it cannot resize the display while in the middle of drawing to it. If you call `setSize()` inside `setup()`, the first point at which you'll have the correct size is when `draw()` runs. 

Running at Full Screen
----------------------

With Processing 3.0, use the `fullScreen()` method to run at full screen. This will create a sketch the size of your entire display. If you just want to sketch the same size and blank the rest of the screen, use Sketch → Present. 

#### Display at full screen

The `fullScreen()` function should always be the first line in `setup()` or (if running in another IDE) it should appear inside of the `settings()` function. If the computer has one screen, the software will open on that screen. If the computer has more than one screen, the software will appear on the screen specified in the “Run sketches on display” option in Preferences (see below). These two examples show how it works:

``` {.Processing}
void setup() {
  fullScreen();
  ellipse(width/2, height/2, height, height);
}
```

Use this version when running from another IDE like Eclipse or IntelliJ:
``` {.Processing}
void settings() {
  fullScreen();
}

void setup() {
  ellipse(width/2, height/2, height, height);
}
```

See the [fullScreen()](https://processing.org/reference/fullScreen_.html) and [settings()](https://processing.org/reference/settings_.html) reference for more information.

In Ubuntu Linux under the default “Unity” desktop environment, it's often 
not possible to cover the screen completely with your Processing sketch.
You can use a second [desktop environment](http://askubuntu.com/questions/65083/what-kinds-of-desktop-environments-and-shells-are-available) which does full screen just fine.
Your mileage will vary as you use different renderers. As of this writing, `FX2D` will properly do full screen mode, however the default renderer will not. 


Using Multiple Monitors
-----------------------

A lot of effort has gone into fixing up support for multiple displays in 2.0 and 3.0.

By default, a full screen application doesn't cover multiple displays.
This is often the preferred solution (for instance, when coding on one
monitor and displaying on another). In some cases (usually involving
OpenGL), using a single sketch across multiple displays may cause it to
run more slowly. This depends on the graphics card, drivers, etc. and is
out of our control.

#### Full screen on any display

The `fullScreen()` function has parameters to define on which screen to run
the software and to span the software across multiple displays as a 
continuous surface. For example, to display full screen on the second display,
use this code:

``` {.Processing}
void setup() {
  fullScreen(2);
  ellipse(width/2, height/2, height, height);
}
```

#### Running a sketch across multiple displays

If you want to use multiple monitors as a continuous window, use
`fullScreen()` and use `SPAN` as the parameter instead of the number
of an individual screen.

``` {.Processing}
void setup() {
  fullScreen(SPAN);
  ellipse(width/2, height/2, height, height);
}
```

See the [fullScreen()](https://processing.org/reference/fullScreen_.html) reference for more information.

#### “Run sketches on display” option in Preferences

The "Run sketches on display" option in the Preferences window 
sets the display where sketches are initially placed. As usual, if the sketch
window is moved, it will re-open at the same location, however when
running in full screen mode through Sketch → Present, the display 
selected here will always be used.

When exporting an application, that display preference will be saved
into the exported application.