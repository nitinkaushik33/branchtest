This page documents a list of ideas and how you can help contribute to the foundation's work on [Processing](http://processing.org), [p5.js](http://p5js.org), and [processing.py](http://py.processing.org).

For all of our projects, it's incredibly important that things are kept as simple and user-friendly as possible. Our work is not for developers, it's for people who are less familiar with code, and/or just want to get things done. We're far less interested in features to make the environments more powerful for advanced users than we are in features that make it easier to handle tasks that are common for a wide range of our audience.

In addition to this list, we are track specific bugs and enhancements via github issues:
* [Processing](https://github.com/processing/processing/issues)
* [Processing documentation](https://github.com/processing/processing-docs/issues)
* [p5.js](https://github.com/processing/p5.js/issues)
* [p5.js documentation](https://github.com/processing/p5.js-website/issues)
* [processing.py](https://github.com/jdf/processing.py/issues)
* [processing.py documentation](https://github.com/kazimuth/processing-py-site/issues)

In particular, you might take a look through all of the [issues tagged enhancement](https://github.com/processing/processing/issues?labels=enhancement&page=1&state=open) as well as those [tagged help](https://github.com/processing/processing/issues?q=is%3Aopen+is%3Aissue+label%3Ahelp) in any of our repos.


## Summer 2017

The Processing Foundation works each summer with students who are interested in contributing to open source. From 2011 through 2015 we participated in Google Summer of Code.  In 2016, we ran an internship program through [ITP](http://itp.nyu.edu) at New York University.  This year we have beeen accepted as a mentoring organization with [Rails Girls Summer of Code 2017](https://teams.railsgirlssummerofcode.org/) and [Google Summer of Code for 2017](https://summerofcode.withgoogle.com/).

### Apply!
* [Rails Girls Summer of Code Application and Info](http://railsgirlssummerofcode.org/)
* [Google Summer of Code Application and Info](https://summerofcode.withgoogle.com/)
* [Processing Foundation Google Summer of Code Page](https://summerofcode.withgoogle.com/organizations/4962961559912448/)

### Previous year GSOC reports
To get a sense of the kinds of project we work on via GSOC, take a look at these reports.
* [Processing Foundation GSOC Page](https://processingfoundation.org/advocacy/google-summer-of-code)
* [GSOC 2014](http://shiffman.net/2014/11/01/gsoc-2014/)
* [GSOC 2013](http://shiffman.net/2013/09/24/gsoc/)

## p5.js

Over the past few years, we have been developing [p5.js](http://p5js.org), a JavaScript library that starts with the original goal of Processing, to make coding accessible for artists, designers, educators, beginners, and reinterpets this for today's web. Using the original metaphor of a software sketchbook, p5.js has a full set of drawing functionality. However, you’re not limited to your drawing canvas, you can think of your whole browser page as your sketch! For this, p5.js has addon libraries that make it easy to interact with other HTML5 objects, including text, input, video, webcam, and sound. p5.js is a new interpretation, not an emulation or port, and it is in active development.

### Strategy / Outreach
* Community outreach initiatives, especially those aimed at reaching and supporting more diverse audiences.
* Studying and improving p5.js community management, with a focus on project and community growth and sustainability.
* Studying and improving p5.js development workflow processes (sometimes referred to as [DevOps](https://en.wikipedia.org/wiki/DevOps)). Of particular need is an automated release process (see the current release steps [here](https://github.com/processing/p5.js/wiki/Release-steps)).
* Improving documentation for contributors, to make it more accessible for beginners.
* Adding [github issue and pull request templates](https://github.com/blog/2111-issue-and-pull-request-templates).

### Improving and Developing Functionality
* __(high priority)__ Continued development of WebGL/3D functionality. See [more info and roadmap](https://github.com/processing/p5.js/wiki/Getting-started-with-WebGL-in-p5#the-future-custom-shaders-shadow-maps-full-featured-virtual-camera-etc). Here is a list of [current open webgl issues](https://github.com/processing/p5.js/issues?utf8=%E2%9C%93&q=is%3Aissue%20is%3Aopen%20webgl).
* Fixing [bugs](https://github.com/processing/p5.js/issues) is an area where we need a lot of help and proposals in this category will be given great consideration. We suggest picking a number of issue reports that pertain to a particular area of the codebase and packaging them as one project.
* Continued development of the [p5.Sound](https://github.com/processing/p5.js-sound/) library.
* Adding and improving [p5.js website](https://github.com/processing/p5.js-website), reference, example generation scripts.
* Continued development of mobile functionality. See [current open issues](https://github.com/processing/p5.js/issues?utf8=%E2%9C%93&q=is%3Aissue%20is%3Aopen%20label%3Aarea%3Amobile%20).

### New Features (lower priority)
* Creating an [addon library](https://github.com/processing/p5.js/wiki/Libraries) for other functionality that could be integrated with p5.js. (Ex: OSC, local storage, database)
* We are currently in the process of building a [p5.js web editor](https://github.com/processing/p5.js-web-editor). See the [issues list](https://github.com/processing/p5.js-web-editor/issues) for ideas.


## Processing

Last month, the desktop version of Processing had 250,000 unique users. Daily, there are 25-30,000 people who make use of the PDE. We want to improve the experience those people have with the software, and need far more people than just the tiny team of contributors.

### Help us with the PDE
* The initial experience of using Processing could be improved. We have 100s of examples, and a better way to get people started with the PDE would be to introduce more of them, along with the tutorials, as part of the initial experience with the PDE. This work might also include improving or expanding upon the tutorials as well.
* The Processing Development Environment (PDE) is currently built in Java, using custom components that make use of Java's “Swing” library, which is even more outdated now than when it was first released. An interesting project would be a prototype replacement for the PDE itself with a JavaScript-based solution that would 1) allow more people to contribute to its further development, 2) provide better support for building the UI, 3) have more visually consistent cross-platform results, and 4) potentially open up other ways to distribute the PDE. Behind the scenes the code would remain Java-based, but rebuilding the UI into something more flexible would be a worthwhile exercise. 
* Implement a better way to understand how people use Processing. We collect stats on the number of people using Processing, what version they're on, what OS, etc. We also collect stats for what people have installed so that we know where to put our efforts for Libraries, Modes, and Tools. At the moment, these are looked at manually (SQL on the command line) when we're trying to make decisions. But it'd be great to have a better way to share these with the community in an ongoing basis (Scratch does a [nice job](https://scratch.mit.edu/statistics/) with this), and also for us to keep an eye on how things are going.

### Python & Python Mode
* [Python Mode for Processing](http://py.processing.org/) allows you to write Processing sketches using the Python programming language.  We are looking for help with [the implementation of Python Mode](https://github.com/jdf/processing.py) and [its documentation](https://github.com/kazimuth/processing-py-site).
* We'd love for someone to take on a native (C Python) version of Processing. While it wouldn't have the advantage of library support that we get from the current Jython-based implementation, it'd open up other ways to extend Processing with Python's syntax, features (numpy, scipy), and considerable base of support.

### Sound
* We could really use more cross-platform help with the [Sound](https://github.com/processing/processing-sound) Library. 

### Video
* The video library for Processing uses an engine built on top of [GStreamer](http://gstreamer.freedesktop.org/). During the previous years there have been different efforts to update GStreamer to more contemporary (1.x) versions, but it has proven to be quite a challenge.
* The most recent contender is the [GL Video library](https://github.com/gohai/processing-glvideo), developed by [@gohai](https://github.com/gohai) in order to get hardware-accelerated video playback to run on the resource-constrained Raspberry Pi computer. As of now, this library runs on the Raspberry Pi, Desktop Linux and macOS. An effort could be made to turn this into a proper replacement for Processing's main Video library, for which it would need to run on all platforms, and work at least equally well as what we have currently. Specific tasks that are left to be done:
 * Implement Windows support ([issue](https://github.com/gohai/processing-glvideo/issues/7))
 * Implement a pixelcopy fallback so that the library can also be used with the default render
 * Work with the gstreamer community to figure out capture device enumeration on macOS and Windows ([issue](https://github.com/gohai/processing-glvideo/issues/8))
 * Finish Capture support ([issue](https://github.com/gohai/processing-glvideo/issues/21))
 * Follow up on bug reports
 * (Caveat: the GL Video library is partially written in [C using JNI](https://github.com/gohai/processing-glvideo/blob/master/src/native/impl.c).)
* An alternative could be to replace the old gstreamer-java bindings in the [current video library](https://github.com/processing/processing-video) with [GStreamer 1.x Java Core](https://github.com/gstreamer-java/gst1-java-core), which has been updated to support gstreamer 1.x. This approach would not require to work with JNI/C code, but might involve adding missing functionality to gst1-java-core (which is JNA-based). 

### Processing for Android
* The ant scripts and android tool have been removed from the latest version of the SDK tools, thus [breaking the mode](https://github.com/processing/processing-android/issues/307). We need to transition to gradle as the internal build system. The mode can already be built using gradle, and it exports sketches as gradle projects, so many elements already in place to start the transition.
* The emulator support is clunky, i.e.: when running for the first time, the mode does not wait for the emulator to start up, the Processing AVDs could be configured better, the latest version of the wear emulator [does not work on OSX](https://github.com/processing/processing-android/issues/309), and AVDs [cannot be created on Linux](https://github.com/processing/processing-android/issues/308).
* A [Google Tango](https://developers.google.com/tango/) library.
* We are incorporating support for [live wallpapers](http://android.processing.org/tutorials/wallpapers/index.html), [watch faces](http://android.processing.org/tutorials/watchfaces/index.html), and [VR (Cardboard/Daydream)](http://android.processing.org/tutorials/cardboard_intro/index.html) in the latest versions of the Android mode. It would be great to see original applications of these new app types on the Android platform. 
* Improving stroke rendering in P2D, right now is ridiculously slow. The reason for this is the stroke geometry is computed using a [highly unoptimized code](https://github.com/processing/processing-android/blob/master/core/src/processing/opengl/PGraphicsOpenGL.java#L11684) in the GL renderer that first produces a line path that is then tessellated using GLU's tessellator. This needs to be done more efficiently, and any improvements will also benefit P2D in the Java mode as the code is shared between the two modes.
* Video/Media library for Processing Android? This would probably wrap the [media engine](http://developer.android.com/reference/android/media/package-summary.html) and [player](http://developer.android.com/reference/android/media/MediaPlayer.html) already available in Android. A former GSoC student developed a [video library](https://github.com/omerjerk/processing-video-android) for the Android mode, supports video playback and camera capture through OpenGL textures for good performance. Perhaps it can be continued/expanded. 

### OpenGL 
* Right now, editing of GLSL shaders is not supported by the PDE. An external tool allowing to code shaders side by side with the sketch code could be very useful and cool.
* Central repository of shaders, probably connected somehow with the editor. Also, an advanced shader tutorial following the introductory one [here](http://processing.org/tutorials/pshader/) is also needed.
* A library for advanced shaders (lighting, geometry, tessellation), that handles the low-level stuff. Right now it is possible to create geometry or tessellation shaders by using the [GL3/GL4 API](https://github.com/codeanticode/pshader-experiments/blob/master/TerrainTess/GL4Shader.pde), but would be nice if that could be handled automatically by this hypothetical library. Also integration with the repository suggested above would be neat.
* A library to do calculations on the GPU using the OpenCL API. This library could work in coordination with the OpenGL renderers to allow handling large particles systems, very complex dynamic meshes, etc. A prototype OpenCL library for an early Processing 2.0 alpha release, which implemented traer.physics solvers with OpenCL kernels, is available [here](https://code.google.com/p/clphysics/).

### Libraries
* Is there something you think Processing should do, but it currently doesn't?  Processing can be extended through [Libraries](http://processing.org/reference/libraries/) and we're always looking for contributions.  Instructions for building libraries are here on the [GitHub wiki](https://github.com/processing/processing/wiki).
* The libraries that allow Processing to communicate with the MS Kinect could use work and updating. See: includes [openkinect](https://github.com/shiffman/OpenKinect-for-Processing).
* The [Toxiclibs](https://github.com/shiffman/toxiclibs) has been updated for Processing 3, but there is work that could be done to fix bugs, improve documentation and examples, and keep aligned with [toxiclibs.js](http://haptic-data.com/toxiclibsjs/).
* Think up your own idea for a library!

### Tools for the Processing Development Environment (PDE)
* There's an [extensive list of potential tools](https://github.com/processing/processing/wiki/Tool-Ideas) on the Processing Wiki that are waiting to be programmed. Instructions for building tools are here on the [GitHub wiki](https://github.com/processing/processing/wiki/Tool-Overview).
    
### Smaller, Isolated Projects and Fixes
There are a number of smaller projects that could be handled by someone who doesn't necessarily want to dive all the way in to the code. Often these are isolated things that we've just never had the time to get around to. We track many of these with the [help label](https://github.com/processing/processing/issues?q=is%3Aopen+is%3Aissue+label%3Ahelp). Please help!