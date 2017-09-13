OpenGL (Open Graphics Library) is a cross-platform graphics interface
for 3D and 2D graphics. This library allows Processing programs to
utilize the speed of an OpenGL accelerated graphics card. This expands
the potential for drawing more to the screen and creating larger
windows. Processing interfaces with OpenGL through JOGL, an initiative
formerly from the Game Technology Group at Sun. For more information,
please visit the [OpenGL](http://www.opengl.org/) and
[JOGL](http://jogamp.org/jogl/www/) websites.

### Changes in Processing 2.0

In Processing 2.0, a new version of the OpenGL library replaces the one
found in 1.x releases:

-   It requires a more recent version of OpenGL, which may cause
    problems on older hardware and/or out-of-date drivers
-   it is now part of the core (no need to use Import Library → OpenGL).
    This simplifies things (enormously), and brings better parity with
    other platforms like Android. This makes exported applications
    larger, but the benefits are worth it.
-   The new library is based on Andres Colubri's Android work (and his
    experiences developing the GLGraphics library). All the great things
    from Android have now been back-ported to the desktop version of
    Processing, so we have a super fast OpenGL library.

### Troubleshooting

-   Try updating your graphics card drivers. If you're getting a blank
    screen with sketch that uses OpenGL, or the sketch is hanging or
    starting very slowly, you likely need to update your drivers. On
    Windows, updated drivers are available from your machine's vendor,
    Windows Update, or the manufacturer of your graphics card. On Mac OS
    X, use Software Update to make sure your system is up to date. On
    Linux, try the non-free version of a driver.

-   On Windows, if you're getting a lot of OpenGL crashing, blue
    screens, or other mess, your driver might be bad (really!) For
    instance, if you're using a Dell, use the driver they provide
    ([<http://support.dell.com/>](http://support.dell.com/)) instead of
    what might be a more recent driver obtained directly from
    [<http://nvidia.com>](http://nvidia.com).

-   If you're getting a blank screen or strange graphics on Windows, try
    messing with your graphics card settings (or even with a different
    graphics card). There are lots of options that can cause trouble (if
    you run into such a situation, please post to the forum on how you
    got it fixed).

-   If you've recently updated, you may, on the other hand, need to
    downgrade your drivers. Sometimes experimental drivers (or the
    “free” drivers on Linux) contain issues. Try different versions that
    might be available for your system.

-   Almost all EXCEPTION\_ACCESS\_VIOLATION crashes with OpenGL are
    driver problems, and we cannot fix them.

-   We don't recommend running other OpenGL programs while running
    Processing in OpenGL mode. GL tends takes charge of things so
    results will be unexpected (windows from the other app showing
    through to the Processing window, etc.)

-   The integrated graphics chipsets that Apple has been using on their
    "low end" machines (such Intel GMA 950) really stink for OpenGL.
    Some don't support anti-aliasing at all. These cards are found in
    the Mac Mini (the Intel version only, the PPC versions had nice
    graphics), some iMacs, and the MacBook (but no the MacBook Pro). The
    same chipsets are used in many budget PCs, to which the same
    disclaimer applies.

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

### Known Issues

-   [OpenGL
    Issues](https://github.com/processing/processing/labels/opengl)
    in the bugs database.