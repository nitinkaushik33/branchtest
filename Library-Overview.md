A Processing library can be any Java code that's been given a package name and packed into a JAR file. It can also register itself with the parent applet to get notification of when events happen in the sketch, for instance whenever `draw()` is called or a key is pressed.

Most libraries may not need that much functionality, but they may want to implement the `dispose()` call, which is called as the applet is closed. Many libraries, especially those with native code, need this to properly shut down.

It is not possible to build libraries from within the Processing application. In fact, **creating a library with the PDE will cause problems** because the JAR file exported from the PDE will contain the current version of the `processing.core` classes, which will cause major conflicts when trying to use any other code. Libraries that contain classes from the `processing` package in this manner will have to be rejected or removed from the site.

The Processing Development Environment (PDE) is built with the sole purpose of creating sketches that are part of `PApplet` that have a few files at most. We don't plan to extend the PDE to also support developing libraries or tools, because then it becomes like any other IDE that is quickly too general for our target audience. Users who are advanced enough in their programming skills to build libraries will almost always be skilled enough to use another IDE like Eclipse to build their library. (And if not, it's a lovely time to learn.)


## Where To Put Libraries

Core libraries live inside the `libraries` folder of the Processing distribution. This folder is not visible on Mac OS X (unless you right-click `Processing.app` and select "Show Package Contents"). All _contributed_ libraries should be installed in the sketchbook folder inside a folder named `libraries`.

If a library works only with a particular release of Processing, then it may make sense for the user to put things into the Processing libraries folder, however we'd like to keep users out of there as much as possible. Telling Mac users to use "Show Package Contents" to install a library is very much frowned upon.


## Build Your Own Library

If you are building your own library, the [Eclipse Library Template](https://github.com/processing/processing-templates/wiki/Eclipse-Library-Template) will help you to get started developing your library with the [Eclipse IDE](http://eclipse.org). The [[Library Basics|Library-Basics]] section will give you a better understanding of how a library works. If you want to share your library with the processing community, please take a look at the [[Library Guidelines|Library-Guidelines]].


## Another Alternative: Using the `code` Folder

If all you want to do is add some Java code to a sketch, sometimes you don't even need to build a full library. If you add a `.jar` file to your sketch (using Sketch → Add File), the file will be copied to a folder named `code` inside your sketch folder. When running the sketch, all packages found in the `.jar` file will automatically be added as import statements in the sketch (though invisible to the user).


## Core vs. Contributed Libraries

There are two categories of libraries. The core libraries (Video, OpenGL, Serial, Net) are part of the Processing distribution, and contributed libraries are developed, owned, and maintained by members of the Processing community.

Occasionally, a contributed library might make its way into the regular distribution. This happened with the Candy library by mflux which eventually became the basis of the SVG parsing used by the `loadShape()` method, or the Minim library by ddf, which is a terrific audio library that's included with the Processing download (but still maintained independently of Processing itself).

The contributed libraries are one of the most important aspects of the Processing project and have an enormous impact on how people use Processing. Libraries have been designed into the larger Processing plan to enable simple extensions of the core API in new, innovative, and unexpected directions. The libraries are the future of the project as we plan for `processing.core` package to remain as minimal as possible. 