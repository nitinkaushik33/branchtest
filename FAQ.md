#### This is broken! I found a bug! Nothing is happening!

Most answers can be found on the [troubleshooting](troubleshooting "wikilink") page, or in the reference for the function or library that you're using. Please read them!

#### How can I obtain Processing and how much does it cost?

The software is free to download and use. Just visit the [download](http://www.processing.org/download/) page.

We think it's important to have Processing freely available, rather than selling it under some godawful yearly contract update scheme. To that end, we encourage people to spread the word and refer them to [processing.org](http://www.processing.org/download/).

#### How do I get started?

Double click the 'Processing' application (on Linux, type ./processing). Select something from File → Examples. Hit the Run button (which looks like the play button on a VCR or tape deck). Lather, rinse, repeat as necessary. More information on using Processing itself is can be found in the [environment](http://www.processing.org/reference/environment/) section of the reference.

For a more detailed overview, check the [Getting Started](http://www.processing.org/learning/gettingstarted/) tutorial. A number of [books](http://www.processing.org/learning/books/) have been written to help, too.

Again, if you're having trouble getting Processing to start, check the [troubleshooting](troubleshooting "wikilink") section of the reference for possible solutions.

#### How do I learn to use Processing?

To learn the Processing language, we recommend you try a few of the built-in examples, and check out the [reference](http://processing.org/reference/). A group of diverse [books](http://www.processing.org/learning/books/) have been written to help people with different goals and skill levels.

When using the examples (or trying someone else's code), if you run across a function that you're not familiar with, highlight the word, right-click (ctrl-click on the mac), and select "Find in Reference" to open the reference page for that keyword. This can be helpful for understanding how programs work.

If you're stuck or want to talk about your work, head over to the [forum](http://forum.processing.org) section of the site to find open minds and helpful peers.

#### I downloaded a new version and my code no longer works!

Read the [revisions.txt](http://processing.org/download/revisions.txt) file that's included with the download (or use that link to read the online version). Things change between releases, and something may have broken your code, or your code may be using something unsupported, which no longer behaves.

#### I'm trying to run some code I found on the web, and it doesn't work

The code may be using syntax from an older release of Processing. Information about updating your code can be found on the [changes](changes "wikilink") between releases page.

Also check [revisions.txt](http://processing.org/download/revisions.txt) to make sure it's not something that's covered there.

#### On what platforms can I run Processing?

We release versions for Windows, Mac OS X, and Linux. We test extensively on Mac and Windows platforms, but not much on Linux.

More detailed information for the specific platforms can be found in the [Supported Platforms](Supported Platforms "wikilink") section, which also includes information about running the Processing Development Environment on other platforms.

#### Is Processing Open Source? How 'bout some code?

The Processing development environment is released as open source under the GPL. The export libraries (also known as 'core') are released under an LGPL license, which means they can be used as a library and included in your project without you having to open up your code (though we encourage people to share anyway). But if you make changes to core, you have to submit back to us. More information about the GNU Public License can be found at [1](http://www.gnu.org/copyleft/gpl.html).

The source code is stored in this [github repository](http://github.com/processing/processing), and more information about its use can be found here.

We need help! Having shared all the code and made it available for free, doesn't it just make you want to pitch in and help? We have too much work to do and can't keep up with things. We love to see bug fixes, new libraries, etc. If you're interested, contact us via the [Forum](http://forum.processing.org) section of the site.

The source code for the libraries is also included with the Processing software itself, should you want to modify them for your own use. If you want to modify the library for your own use, you can include the .java file as part of your sketch. Just be sure to remove the "package processing.xx;" line at the beginning. The Processing environment does not allow packages.

Processing also relies on (and is indebted to) other open projects, namely:

-   the jEdit Syntax package, which is public domain
-   the ECJ Compiler from the Eclipse project, which uses the Eclipse license.
-   the Java Native Access (JNA) project, released under the LGPL.
-   as of release 0149, we use a slightly modified version of launch4j to create processing.exe on Windows.
-   the quaqua library, which makes Java applications look more like Mac applications when running on OS X.
-   ...perhaps others, let us know if we're missing something.

The following are no longer in use, but we still owe them because they helped us along in earlier releases:

-   the older ORO Matcher, distributed under a BSD-style license as part of the Apache Jakarta project
-   the Jikes compiler, which is covered by the IBM Public License.
-   com.ice.jni.registry from the Giant Java Tree (GPL license)

#### Do I have to cite Processing? Do I have to share my code? Can I distribute my sketches?

We like it when people include a "Built with Processing" note with a link back to the site, since it helps create interest and brings in more people to the project. We don't/can't/shouldn't require it, but it makes us happy because the project is free and this is one way you can help give back to us.

You can also remove the source code from web pages that you export, but in the spirit of the Processing project overall, we include it by default so as to encourage sharing and learning from one another.

You can distribute your sketches all you want, and commercial projects are just fine too, however we place no warranty on the software (see the download page for the license shenanigans).

#### What's with the version numbers?

An "alpha" release means we're still breaking things. A "beta" release means that the API is locked up for the final, but not all the bugs are necessarily worked out. Beta also means that we think it's stable enough for day-to-day use, and clearly better than the previous release. For instance, we believe the 3.0 beta releases to be in better shape and have fewer bugs than the 2.2.1 release that's well over a year old. 

Releases prior to 1.0 were numbered with four digits. Revision 0069 was the last alpha release, revision 0085 was the first "beta" release, and revision 0161 was the last beta. Under the old numbering system, release 1.0 is 0162. With the 2.0 series, we've mostly dispensed with using the revision numbers to avoid confusion.

#### Why is it called “Processing”?

At their core, computers are processing machines. They modify, move, and combine symbols at a low level to construct higher level representations. Our software allows people to control these actions and representations through writing their own programs. The project also focuses on the “process” of creation rather than end results. The design of the software supports and encourages sketching and the website presents fragments of projects and exposes the concepts behind finished software.

“Proce55ing” is the spelling we originally used for the URL of the web site, because "Processing" was already taken. Even though it's a combination of numbers and letters, it was always pronounced “processing.” Since then, we saved our pennies, had a can drive, and used the funds to acquire the processing.org domain name. As a result we are no longer using the name “Proce55ing.”

When we see it with the 55's it annoys us and we want to punch people in the face. Or punch ourselves in the face for using it in the first place. Actually, we try not to be that emotional about it but we're trying to avoid the previous naming. However, to make it more confusing, we sometimes still use “p5” (but not p55!) as a shortened version of the name.

#### What is the sketchbook? What do you mean by sketches?

We think most “integrated development environments” (Microsoft Visual Studio, Xcode, Eclipse, etc.) tend to be overkill for the type of audience we're targeting with Processing. For this reason, we've introduced the 'sketchbook' which is a more lightweight way to organize projects. As trained designers, we'd like the process of coding to be a lot more like sketching. The sketchbook setup, and the idea of just sitting down and writing code (without having to write two pages to set up a graphics context, thread, etc.) is a step towards that goal.

The idea of just writing a short piece of code that runs very easily (via a little run button) is a direct descendant of John Maeda's work in Design By Numbers, and our experiences maintaining it. (Yes, other languages and environments have done this first, but in our case, the concept is drawn from DBN.)

#### Why Java? Or why such a Java-esque programming language?

We didn't set out to make the ultimate language for visual programming, we set out to make something that was:

1.  A sketchbook for our own work, simplifying the majority of tasks that we undertake,
2.  A teaching environment for that kind of process, and
3.  A point of transition to more complicated or difficult languages like full-blown Java or C++ (a gateway drug to more geekier and more difficult things)

At the intersection of these points is a tradeoff between speed and simplicity of use. i.e. if we didn't care about speed, Python, Ruby or many other scripting languages would make far more sense (especially for the simplicity and education aspect of it). If we didn't care about transition to more advanced languages, we'd get rid of the C-style (well, [Algol](http://en.wikipedia.org/wiki/Algol_60), really) syntax. etc etc.

Java makes a nice starting point for a sketching language because it's far more forgiving than C++ and also allows users to export sketches for distribution across many different platforms. When we got started in 2001, most people were using it to build [applets that ran on the web](http://processing.org/exhibition/curated_page_1.html), which was important to the early growth of the project.

Processing is not intended as the ultimate environment or language (in fact, the language is just Java, but with a new graphics and utility API along with some simplifications). Fundamentally, Processing just assembles our experience in building things, and trying to simplifies the parts that we felt should be easier.

#### I know Java, is this Java? How do I use it that way?

Processing code is converted to straight Java code (using the "preprocessor") when you hit the Run button. This also makes it possible to embed other Java code in your sketches, or use the core.jar file from the Processing distribution to develop your own sketches with other environments. For instance, if you want to use [Eclipse](http://eclipse.org/), there's a [tutorial](http://processing.org/learning/eclipse/) on the Processing site.

The main rule when using Java code: You cannot use most of the AWT or Swing (which is built on the AWT), because it will interfere with the graphics model. If you want to add scroll bars and buttons to your projects, you should make them using Processing code, or embed your Processing applet inside another Swing or AWT application (see below). Even if they appear to work, such sketches will usually break when you try to run on other operating systems or other versions of Java.

Since we can't really support anything and everything that you might want to do when interfacing with Java or using core.jar inside a Java environment, we have a separate [discussion area](http://forum.processing.org/two/categories/hardware-other-languages) on the discourse forum for asking questions related to using Processing to interface with regular Java code.

If you want to embed Processing into another Java application, visit the developer's reference for [PApplet](http://dev.processing.org/reference/core/javadoc/processing/core/PApplet.html). A discussion of how to use Processing with Eclipse is found [here](http://processing.org/discourse/yabb2/YaBB.pl?board=Integrate;action=display;num=1117133941).

Also note that when using the Processing API or libraries outside the PDE, the headaches of the Java CLASSPATH and PATH return, and using libraries gets much nastier. These are some of the headaches that we try to hide in the Processing environment, things that separate Processing from straight Java coding. We feel that it is important to put the good stuff at the surface, and that those details don't teach students much anyway (and they annoy advanced users too).

#### Where does this project come from? Is this DBN?

Processing is a descendant of the [Design By Numbers](https://web.archive.org/web/20030923172031/http://dbn.media.mit.edu/) (DBN) project and other initiatives at the Aesthetics + Computation Group (ACG). DBN is a simplified programming language that was developed to teach the structure and interpretation of software in a visual manner. Design By Numbers was created by John Maeda and accompanied a book of the same name. While at the ACG, Ben and Casey were involved in the development and maintenance of the DBN software and courseware, and that experience provided the basis for the Processing project.

While working on DBN, Ben developed several experimental versions that included other programming languages (Python and Scheme) and drawing features (color, changing the window size, magnification, movie recording, and even OpenGL support), but it was clear that these did not make sense for the DBN project because they interfered with Maeda's intention of a simplified programming language and environment.

At the time (between 1998-2000), work at the ACG was usually developed via sketches written in Java and later moved to applications written in C++ using OpenGL. We were interested in melding the idea of "sketching" in code with the pedagogical aspect of DBN. Development of Processing began formally in the Spring of 2001 with discussions between Casey and Ben about API and feature set, and the first few versions of Processing (releases 0001, 0003, and 0005) were used in August 2001 at a [workshop](http://dbn.media.mit.edu/workshops/musabi/) at Musashino Art University in Japan.

#### Checking for updates, or “why is Processing connecting to the network?”

After you double-click Processing, it will check the site for updates. This is helpful so that we can keep people aware of the frequent updates to Processing.

In so doing, it also sends a random number that identifies yours as a unique machine (but sends no personal information to us). This really helps us get a general idea of how many people are using the software, which is very important for things like writing grants so that we can keep Processing free.

Starting with Processing 3, we also send a list of what Libraries, Modes, and Tools that you have installed. We added this because it was difficult during the 3.0 release process because we had no information about what's used most commonly across the hundreds of thousands of people who use Processing. We wanted to figure out where to concentrate what little volunteer time we had toward helping authors of contributions to get them updated, or knowing when we might need to pick up the slack if an author had disappeared.

If the network connection causes you trouble, or if you're ~exceptionally paranoid~uncomfortable with sharing the list of things you've installed using the Contribution Manager (the dialog box that shows up when you do "Add Library..." or "Add Mode..."), it can be shut off inside the Preferences window. Shutting off the update checks also means that the Contribution Manager will not work, because it needs access to the network as well. This also means that you'll need to manually install Libraries, Modes, and Tools.