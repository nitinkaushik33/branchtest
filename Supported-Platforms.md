This page describes our relationship to macOS, Windows, and GNU/Linux. Scroll to the bottom, and you can even read about different versions of Java.

The Processing Development Environment (PDE) is currently tested on:

1.  macOS 10.12
2.  Windows 10 (64-bit)
3.  Ubuntu Linux 16.04 (64-bit)
4.  Windows 7 (32-bit and 64-bit)
5.  Ubuntu Linux 14.04 (32-bit)

This list is ordered by what gets the most testing, with primary development happening on macOS. Most of the cross-platform work is done from a certain developer's laptop that has seven or eight VMware images to deal with all this mess. 
Things that can't be tested from a VM are run from machines at the Processing Release Testing And Quality Assurance Center (the PRTAQAC, which is currently a number of machines laying about [Fathom's studio](http://fathom.info)).

*Also check out the [Troubleshooting](Troubleshooting "wikilink") page for platform-specific issues.*

Windows
=======

Windows is generally the the best platform for running Java
applications. It's not because we like Windows (we don't) but that's
just how it is.

Windows 7 and later is supported. No XP, no Vista.

Most testing happens on Windows 10, with some additional on 7. Very little testing happens on Windows 8. When we do, we only use the latest version (8.1).

Some editions of Windows Server are reported to work, but are not supported.

Mac OS X
========

Java on Mac OS X has always dragged behind other platforms.

-   Starting May 2017, macOS 10.12 will receive the most testing. If you're
    using an earlier version, you should consider upgrading because even
    Apple is aggressively dropping support for earlier versions.

-   Mac OS X 10.8.5 or later is required to run Processing 3. Mac OS X
    10.11+ is recommended. A 64-bit machine is also necessary.

-   Processing 2 was the last version to support OS X 10.7.

-   Starting with Processing 2.1, we are no longer using Apple's
    (deprecated) version of Java and have switched to the Oracle
    release. This means:
    -   Processing is only 64-bit on OS X, because Oracle's Java only supports 64-bit machines.
    -   There will be bumps in the transition. Help me fix them.
    -   The download size is larger, because an entire JRE has to be embedded.
    -   There are some performance losses with graphics because the graphics engine in Oracle's version isn't optimized as well as Apple's was. There's a lot of work in Processing 3 to address these issues, including better OpenGL support and the new `FX2D` renderer. Those might be an option if you're having performance problems.

- Apple has long since discontinued support for their version of Java that was used on older versions of Processing. In fact, it won't even be available in future versions of OS X. As such, it's especially important to move things from Processing 1.x and 2.x up to 3.0. More information, straight from [the horse's mouth](https://developer.apple.com/library/prerelease/mac/releasenotes/General/rn-osx-10.11/index.html):
  > OS X v10.11 is the last major release of OS X that will support the previously deprecated Java 6 runtime and tools provided by Apple. Applications or features that depend upon Java 6 may not function properly or will not launch when Java 6 is removed.

-   The key conventions in Processing are closer to other programmer's editors
    on OS X (TextWrangler, Eclipse, etc) than other OS X defaults. This makes some people
    unhappy. Those people can manually edit preferences.txt (its
    location is listed in the Preferences window) to change a line or
    two:

```
 # The home and end keys should only travel to the start/end of the current line.
 # The OS X HI Guidelines say that home/end are relative to the document.
 # if this is not to your liking, this is the preference to change:
 editor.keys.home_and_end_travel_far = false

 # The home and end keys move to the first/last non-whitespace character, 
 # and move to the actual start/end when pressed a second time. 
 # Note that this only works if editor.keys.home_and_end_travel_far is false.
 editor.keys.home_and_end_travel_smart = true
```

#### Retina Support

For Processing 3, use the `pixelDensity()` command to enable super-crisp rendering on retina displays. [See here](http://beta.processing.org/reference/pixelDensity_.html) for the reference.

Linux
=====

With any luck, the Linux release should work fine by simply changing to
the processing folder and typing

` ./processing`

Most problems on Linux come from the version of Java that's included in
the download being incompatible with the OS. In that case, remove (or
rename) the included ‘java’ folder, and replace it with a usable version
of JRE 8. You can also symlink it to a JRE that's installed on your
machine. Be sure that the symlink is set up relative to the ‘processing’
shell script such that ./java/bin/java points to the ‘java’ binary. Take
a look at the folder structure of the included ‘java’ folder to see how
it works.

~~If you replace the 'java' folder, you'll lose the default fonts used for
the PDE. You can get them back by copying the “SourceCode” items from
the included java/lib/fonts folder to your new java/lib/fonts.~~
This is [no longer the case](https://github.com/processing/processing/pull/4639) in releases later than Processing 3.2.1.

Due to incompatibilities, **OpenJDK is not supported.** You'll need a
regular Java release downloaded from Oracle. The GNU Classpath, GCJ,
GIJ combination will not work with Processing. OpenJDK and IcedTea also
have problems, particularly with running sketches full screen or with
multiple displays or even window sizing. Bottom line: use the version
from Oracle.

Information on how to install Java from Oracle on Ubuntu can be found here:
https://help.ubuntu.com/community/Java.

If you get Processing to run properly, the Sketch → Show Sketch Folder
command may not be available. Processing will attempt to find xdg-, kde-,
and gnome-open, and if none is available, the menu item will be
dimmed. To fix this, you must set a launcher for your platform. Add a
line to \~/.processing/preferences.txt that specifies its location:

`launcher.linux = /path/to/launcher_app`

To install on Ubuntu Linux 14.04:

- Download the latest installation (processing-3.2.1-linux64.tgz, for example)
- Open a terminal
- Copy the installation to your home folder
- Extract using: tar zxf processing-3.2.1-linux64.tgz
- Run using ~/processing-3.2.1/processing
- The splash screen and application should now be displayed

To add an Ubuntu launcher icon:

- Run as above
- Select the icon in the launcher
- Right click and select 'Dock to Launcher'
- Close the application
- Open a terminal
- Run 'vim .local/share/applications/processing.desktop' (or use 'nano' in the place of 'vim')
- Use the following lines to replace the existing ones, with your login name in the place of 'mylogin'
```
    Icon=/home/mylogin/processing-3.2.1/lib/icons/pde-48.png
    Path=/home/mylogin/processing-3.2.1
    Exec=/home/mylogin/processing-3.2.1/processing
```

ARM Linux
=========

#### Devices

For new devices, please start a new page:

* [Raspberry Pi, Pi 2, Pi 3, Pi Zero](Raspberry-Pi)
* [C.H.I.P.](C.H.I.P.) *in progress*
* [DragonBoard410c](DragonBoard410c) *in progress*

#### FX2D

The experimental FX2D renderer is not supported on ARM, because Oracle dropped support for JavaFX on ARM devices with Java 8u33. We might want to try using [OpenJFX](http://openjdk.java.net/projects/openjfx/) project in the future, but as of now this is unsupported.

#### Libraries

Most libraries from the Contribution Manager work just fine without any change necessary to run on ARM. Exception to this are libraries that comes with parts written in "native code", which is platform- and architecture-dependent, and hence needs updating. As a general rule of thumb: if you find (sub-) directories for different platforms inside the library's `library` directory, then this is likely the case.

If you come across a library that's not working, or if you need help compiling a library for ARM, please open an [issue](https://github.com/processing/processing/issues/new?labels=arm&assignee=gohai).

#### Library: OpenCV

ARM devices are supported by Greg Borenstein's [OpenCV library](https://github.com/atduskgreg/opencv-processing) starting with version 0.5.4 (available in the Contribution Manager).

#### Library: OpenKinect

A test version of [Open Kinect for Processing](http://shiffman.net/p5/kinect/), with support for armv6hf, can be found [here](http://sukzessiv.net/~gohai/p5-arm/processing-openkinect-arm-fixes-4d25eb2.zip). (PR [#1](https://github.com/shiffman/OpenKinect-for-Processing/pull/46) [#2](https://github.com/shiffman/OpenKinect-for-Processing/pull/50)) On most ARM devices this will only work (if at all) with the Kinect 1, because of the high demand on USB throughput of the Kinect 2. Don't forget to place the file [51-kinect.rules](https://raw.githubusercontent.com/OpenKinect/libfreenect/master/platform/linux/udev/51-kinect.rules) in `/etc/udev/rules.d` for Processing to be able to access the Kinect's camera.

#### Library: PureData

The [puredatap5 library](https://github.com/libpd/puredatap5/raw/3abdfad807365259e7378b3c2f9ddce392f93738/pdp5.zip) allows you to write sketches in Processing that control and interact with musical patches prepared in Pure Data. See the accompanying HelloPd example for how it works. This library requires `PortAudio` to be installed, which seems to be the case for current releases of the Raspbian distribution. This library is not yet available through the Contribution Manager, but support for ARM was merged into its main [repository](https://github.com/libpd/puredatap5). 

#### Library: Processing Sound

ARM devices are supported by Processing's [Sound library](https://github.com/processing/processing-sound) starting with version 1.4.0 (available in the Contribution Manager).

#### Library: Simple Touch

The [simpletouch library](https://github.com/gohai/processing-simpletouch/releases/download/latest/processing-simpletouch.zip) makes it possible to use any multi-touch-enabled display or trackpad with Processing, as long as the device is supported by the Linux kernel. This library is available through the Contribution Manager under the name "Simple Touch".

[Two example sketches](https://github.com/gohai/processing-simpletouch/tree/master/examples) the library comes with explain how to use it. Please file issues [here](https://github.com/gohai/processing-simpletouch/issues/new).

#### OpenJDK

Processing is designed (and supported) to run on Oracle Java. The tar-ball comes with a recent version of Oracle's runtime for hard-float ARMv6 (and higher) architectures.

Other Platforms
===============

Because Processing is written in Java, it should run on any platform
that supports Java 8. If you'd like to get it running on BSD, Irix,
AmigaOS, BeOS... whatever, do the following:

1.  Download the Linux version, and replace the “java” folder with
    versions that support your platform. (See the Linux instructions
    about linking to a proper JDK).
2.  Next, mess with the shell script if necessary to get things up and
    running.
3.  If you have success, share the details for others.

#### OpenBSD

Users of OpenBSD can use the ports and packages framework to install
Processing using the following command:

`pkg_add processing`

Please note this package is not created by the Processing team and any
possible issues should initially be reported to the package maintainer.

Java Versions
=============

**It's never necessary to install Java to use Processing.** Across all platforms, Processing uses its own copy of Java that's embedded inside the application.

We [don't yet support](https://github.com/processing/processing/issues/3054) any of the Java 7 and Java 8 language features. [Please help us fix this.](http://github.com/processing/processing) Advanced users (loosely defined as “people who know that these features exist”) can always make use of Java 7 and 8 features from another IDE.

People often reinstall Java when they have problems with Processing. Even though it may make you feel better, reinstalling won't help anything, because Java doesn't need to be installed in the first place.

### Java 8

Processing 3 uses Java 8. As of April 2015, Oracle is no longer fixing bugs in Java 7, so we had to make the switch.

### Java 9 

Ha! No.