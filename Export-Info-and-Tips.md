### Application Export

Processing can export Java Applications for Linux, macOS, and Windows platforms. When the “Export Application” button is pressed or “Export Application” is selected from the “File” menu, a dialog box opens and you can select whether you want the application to run in Presentation mode along with other options. A folder will be created for the application, the source code for the sketch, and all required libraries will be embedded

Some hints and notes follow below. If you find problems, [file a bug](https://github.com/processing/issues).

-   Starting with Processing 2.1, the Java runtime (JRE) can be embedded
    with exported applications. The positive side of this is that it
    makes the application much more likely to behave exactly as it does
    when run from the PDE, and that users of the exported application
    won't have to install anything additional. The downside is that
    exported applications are much larger (\~100 MB), and the export
    command takes more time. **We strongly recommended that you 
    embed Java with your application.** Not including it opens a pandora's
    box of problems that can happen when people try to run your project.

-   An application for Mac OS X can only be exported from OS X. This is
    due to the complexity of how Oracle's JDK works on OS X, and
    the limitations of the appbundler that we use.

-   The "application.xxxx" folders will be removed completely during export 
    (unless you turn off that behavior in the Preferences window).

-   It is important that you don't have a method named `main()` in your
    sketch, because it will fool the preprocessor into thinking you have a
    clue, when in fact you don't.

-   If the code in your sketch starts `public class blah
    extends PApplet`, you'll need to write your own main() method in
    order for Export to Application to work. It should look something
    like this:

    ``` {.processing}
    static public void main(String args[]) {
      PApplet.main("YourClassName");
    }
    ```

    Writing your own `main()` method is a bad idea and almost certain to 
    break your sketch.

-   The Mac OS X export is a nice .app bundle like a regular OS X
    application. You can change the icon or edit its settings by using
    "Show Package Contents" and editing Info.plist or replacing
    sketch.icns with something more exciting.

-   On OS X, you can also customize the exported application
    automatically by copying the `Info.plist.tmpl` file from inside the
    Processing.app package into your sketch. Any changes made to that
    copy of `Info.plist.tmpl` will be used whenever that sketch is
    exported.

-   On Windows, use this code to set the icon used in the title bar:

    ``` {.processing}
    PImage titlebaricon = loadImage("myicon.png");
    surface.setIcon(titlebaricon);
    ```

-   Linux is just a shell script, which can probably be used on most
    Unix platforms (there's almost nothing to it).

-   When distributing your application, the "source" folder can be
    removed from the export if you'd like, but other files (such as the
    lib folder and any .dll files or whatever) should be left intact
    otherwise the application will not work.

-   Library writers can now specify what files to export for each
    platform, see the [[Library-Basics]] page for more information.

-   Your current memory settings will be exported with the application.
    If you've set outrageous memory requirements, you might want to undo
    that before exporting for others, or edit the exported files by hand
    (Contents/Resources/Info.plist on Mac OS X and lib/args.txt on
    Windows).

-   If you want to replace (or add) titlebar text, just do this in
    setup():

    ``` {.processing}
    surface.setTitle("This is in the titlebar!"); 
    ```

### Presentation Mode Features

The Presentation Mode simply clears the rest of the screen when running the sketch. You can set the default background color (for the area around your sketch) in the Preferences window. 

-   The ESC key will quit a sketch, even in Present mode. To prevent
    this from happening, intercept the ESC on keyPressed() so that it
    isn't passed through to PApplet. Use the following code to prevent
    ESC from quitting the application:

    ``` {.processing}
    void keyPressed() {
      if (key == ESC) {
        key = 0;  // Fools! don't let them escape!
      }
    }
    ```

-   You can hide the stop button with the `--hide-stop` command line
    option to `PApplet`. More details about command line options are above
    in the "Export to Application" section. From inside the Processing
    environment, you can't hide the stop button (unless your sketch
    window obscures it anyway) easily, so better to export as an
    application.