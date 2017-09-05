If you have questions about the contents of this document, ask them in [the forum](http://forum.processing.org/two/categories/developing-processing).

## The quick version

Let's try the easy route first:

* Install Java 8
    * On Windows and Linux, install the latest [JRE 8](http://www.oracle.com/technetwork/java/javase/downloads) from Oracle. 
    * On Mac OS X, download and install [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads). 
    * Previous versions of Java are [not supported](https://github.com/processing/processing/wiki/Supported-Platforms#java-versions).
    * OpenJDK is also [not supported](https://github.com/processing/processing/wiki/Supported-Platforms#linux)

* Install [Apache Ant](http://ant.apache.org/), using their instructions.
    * Ant 1.8 or later is required.

* Clone the [source repository](http://github.com/processing/processing) from Github. 
    * On the command line, enter:
    ````
    git clone https://github.com/processing/processing.git
    ````
    * You can probably use [Git for Windows](http://windows.github.com/) or [Git for Mac](http://mac.github.com/) instead of the command line, however these aren't tested/supported and we only use the command line for development.

* When building for the first time on Windows and Linux, you'll need to have an internet connection, because additional files need to be downloaded. 

* In Processing 3, examples are not included in the build by default. You'll have to clone [processing-docs](https://github.com/processing/processing-docs) alongside the processing folder if you want to use the examples.

* Open a terminal/console/command prompt, change to the directory where you cloned Processing, and type:
    ````
    cd build
    ant run
    ````
With any luck, there will be all sorts of console spew for a few moments, followed by a Processing window showing up. Hooray! 

To get the latest updates, just run `git pull` from the command line (or GUI client) and do `ant run` from inside the `build` folder as shown above.

## That didn't work

Oh well, here are more details for what may have gone wrong: 

* *Remove the work folder* - If it was working in the past, try removing the `work` folder. On OS X, that's build/macosx/work, on Windows, it's build/windows/work, and so on. When larger changes occur, sometimes an old work directory can cause problems. 

* *Try cleaning your build* - Similarly, using `ant clean` will fix many of the weirdest build errors. In fact, you may want to start fresh every once in a while by typing `ant clean`. Then `ant run` will do a new build from scratch.

* *Make sure that `java` is available.* From any terminal/console/command prompt, and type `java` and see what happens. If it says something like `command not found`, then it may be the case that
 * Java may not be installed (did you _really_ skip the first line of the instructions above?)
 * The wrong version of Java is installed (32-bit instead of 64-bit, or vice-versa)
 * The `java` command is [not in your system's PATH](http://www.java.com/en/download/help/path.xml). 
 * Computers don't like you.

* *Make sure that `ant` is available.* Do the same steps as with `java`, above. 

* *Are you behind a proxy?* If you are working in a proxy environment use `ant run -autoproxy`.

* When running ant, the warnings about `unable to locate tools.jar` and mentions of `JAVA_HOME` not being set can be ignored. It's not necessary to set `JAVA_HOME` to build Processing. (Before Processing 2.1, it was necessary. No longer.)

* The build process on Windows and Linux will download its own JRE from Oracle so that it's using the correct/tested version. We only support one version of Java for each release. This helps minimize the already ridiculous number of variables we already have to test against. 

## A faster download

If you're using Git 1.9 or above, you can optionally “shallow clone” repositories using git's `--depth` option. The download size is reduced to ~50 MB (instead of the full 1.5 GB for the main repo). See [this link](http://stackoverflow.com/questions/6941889/is-git-clone-depth-1-shallow-clone-more-useful-than-it-makes-out) for more.

````
git clone https://github.com/processing/processing.git --depth 1
````
The above command will fetch the history of just the latest commit instead of all the commits of the last 14 years. A shallow clone is helpful if you're planning to submit a quick patch. Git 1.9 is relatively new, so you'll probably need to update your git installation before using this option.

## Platform Specific Notes

Happily, each of the platforms we support is different. That means we do extra work to make things work everywhere.

### Mac OS X Notes

* The Mac build requires a specific version of Java. Here's the setting inside `build.xml`:
```
  <property name="jdk.version" value="8" />
  <property name="jdk.update" value="51" />
  <property name="jdk.build" value="16" />
```
That means it'll go looking for JDK 8u51 on your system. You can change that value to something higher than 51, if that's what you're using. Keep in mind that there may be incompatibilities. I'll leave the `jdk.build` entry as a little puzzle to figure out on your own for those determined to use their own JDK. (If you use the latest JDK 8u60, smoothing in FX2D is switched off. See https://github.com/processing/processing/issues/3795)
* A full JDK 8 is required (unlike Windows or Linux, where a JRE is enough). In Processing 3, we moved to Java 8, because support for Java 7 ended in April 2015. Apple's Java 6 no longer works. 
* Installing Xcode is recommended. After installing Xcode, be sure to add the command line tools. This is in Preferences → Downloads → Command Line Tools.
* We use a modified version of Oracle's appbundler project to bundle the Processing application (and as a skeleton for exported applications). You can browse the code [here](https://github.com/processing/processing/tree/master/build/macosx/appbundler). 
 * The `appbundler.jar` file created by that build process is included in the Processing source, so that it's not necessary to have a full Xcode tools installation just to build Processing. 
 * To build appbundler, you'll need a full Xcode installation. You'll also need the OS X 10.10 SDK installed so that the necessary header files are present. (Older or newer versions will not work.)

### Windows Notes 

* Since Processing 2.1, a full JDK is no longer required on Windows. Only the JRE is necessary.
* The trickiest thing on Windows is usually adding `ant` to the PATH and installing the right 32-bit or 64-bit Java that will work from the Command Prompt or whatever shell you're using. To test, type `java` in the Command Prompt (or whatever shell you're using) and see if it picks up your JRE installation. If it doesn't, then you may be using a 32-bit shell and a 64-bit JRE, or vice versa.

### Linux Notes

* Since Processing 2.1, a full JDK is no longer required on Linux. Just the JRE.
* Use Oracle's Java. We don't test with OpenJDK, and over the years it's been problematic. Please just download the version of Java from Oracle. You may think that Oracle is evil incarnate and that the name is an acronym for “One Rich Asshole Called Larry Ellison”. However, this saves me time because you won't be filing bugs about OpenJDK quirks breaking the build or Processing itself.

### Other Notes

* No guarantee is made about the stability of the source on Github. Because almost all development is done by one or two people who are doing this in their free time, we don't work in branches or make excess effort to keep the source stable. 

## Building with Eclipse

_**Disclaimer:** Processing is intended to be built with ant from the command line. Using Eclipse isn't fully supported and may break from time-to-time. You should always ensure the code compiles with ant before submitting a pull request._

1. Open Eclipse, select File → Import... Expand the “Git” folder, select “Projects from Git”, and hit the Next button.

2. On the “Select Repository Source” screen, choose “URI” and enter https://github.com/processing/processing.git
And then click Next.

3. Select “Import existing projects” on the “Wizard for project import” page. Hit Next.

4. Select all the projects shown and finish the wizard. 

5. You'll have several errors, because you need to build the projects once with ant (on the command line: cd /path/to/processing/build && ant) so that the “generated” folder is created. After doing that, select the processing-app project in Eclipse and hit F5 to refresh it.

6. Use Run as Application to start processing/app/Base.java, and you should be in business.

### Notes

  * When building the Android project, you'll also need to set an ANDROID_LIB classpath variable (Preferences → Java → Build Path → Classpath Variables), that points at the android.jar file for SDK 10. i.e. /path/to/android-sdk/platforms/android-10/android.jar

  * For bonus points, you can also set `processing/build/formatter.xml` as the code formatter for your workspace. This is an incomplete implementation of the style guidelines, but it's a start. (Anyone want to [help fix this](https://github.com/processing/processing/issues/3426)?)

  * Be sure the Eclipse execution environment is set to Java 1.8, since that's what's used for the PDE. 

  * Make sure your working directory is set to `processing/build/<platform>/work` if you want to run Processing from Eclipse for debugging.