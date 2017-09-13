# PDE GSOC

## Rough Schedule
* May 19 - June 1: PDE work in 2.x, 3.0 work in PDE X
* ~~June 5: shallow fork Github repo into processing3?~~ 
* ~~June 5: split to 3.0, all work happens in 3.0 from now on~~
* ~~June 6: first alpha release~~
* ~~PDE X as the default (called "Java")~~
* ~~old Java mode still available (called Java 2)~~
* ~~video as its own library~~
* ~~sound library swap~~
* ~~June 23: GSOC Midterm~~
* **Aug 18: GSOC Final and beta code deadline**
   * PVector chaining TBD
   * **PApplet no longer subclasses Applet**
   * **new GUI for PDE**
   * Release 3.0 beta, make it the default download
* Aug ???: 3.0 release?

## Manindra / Dan
* Outstanding items
   * ~~cntrl-space for code completion not working on mac: [2699](https://github.com/processing/processing/issues/2699)~~
   * **streamline code completion: [2681](https://github.com/processing/processing/issues/2681)**
   * ~~**massage real-time error checking timing: [2677](https://github.com/processing/processing/issues/2677)**~~
   * ~~shouldn't write sketch.properties unless it's a non-default mode [2531](https://github.com/processing/processing/issues/2531)~~
* PDE X Robustness
   * ~~Code completion doesn't always work for local variables [exp#68](https://github.com/processing/processing-experimental/issues/68)~~
   * ~~Memory management [exp#1](https://github.com/processing/processing-experimental/issues/1)~~
   * Breakpoints in classes [exp#47](https://github.com/processing/processing-experimental/issues/47)
   * ~~Matching offsets between PDE Code and Java code~~
       * Initial implementation complete. Now on the look out for related bugs.
       * Updated scroll to definition, show usage and refactoring implementations to use the new offset matching. Initial tests look good.
       * Precise error highlighting is here!
   * ~~build instructions wiki for PDE X. no longer relevant when PDE X takes over?~~
   * ~~256 MB Heap Size -- Fry to do~~
* PDE Menu items prior to Alpha Release
   * ~~Separate Debug Menu for Debugger related items. Shall remain hidden on first start up. [exp #71](https://github.com/processing/processing-experimental/issues/71)~~
   * ~~Move PDE X menu items into one of the default menus [exp #72](https://github.com/processing/processing-experimental/issues/72)~~
* Transition PDE X to 3.0 Alpha Release (June 15 target date)
   * ~~processing-experimental code base merged into processing~~
   * ~~Make PDE X the default mode for next alpha release~~
* ~~Added option to disable auto code completion. It can be triggered manually by Ctrl(Cmd) + Space, via a Preference toggle.~~
* Better error messages
   * ~~Dan to help in identifying the common error types, messages would be converted to something simpler and jargon free.~~
   * ~~Error message substitution implemented~~
   * **Find and re-write more messages [47](https://github.com/processing/processing/issues/47)**

## Joel / Florian
* ~~2.0 and 3.0 contributions [PR #2746](https://github.com/processing/processing/pull/2746)~~
* Small items
    * ~~list of open sketches in the menu (a la photoshop)~~ Merged: [PR #2551](https://github.com/processing/processing/pull/2551)
    * ~~add present mode (fullscreen) background color to preferences window #69~~ Merged: [PR #2568](https://github.com/processing/processing/pull/2568)
    * ~~auto-save [2286](https://github.com/processing/processing/pull/2286)~~ Merged: [PR #70](https://github.com/processing/processing-experimental/pull/70)
* Contribution Manager: add anything related to [this milestone](https://github.com/processing/processing/issues?milestone=1&state=open) please
    1. ~~examples manager needed for books, courses, workshops [#2582](https://github.com/processing/processing/issues/2582)~~ 
    2. ~~“starred” / “recommended” libraries [#2580](https://github.com/processing/processing/issues/2580)~~ 
    3. ~~fail more gracefully if no internet connection or a proxy server is in use [#2426](https://github.com/processing/processing/issues/2426)~~ 
    4. ~~different lists for different versions of processing [#2581](https://github.com/processing/processing/issues/2581)~~ 
    5. go through existing tool contributions with Elie (are there outdated tools?) 
    6. Guidelines for modes [#1656](https://github.com/processing/processing/issues/1656) 
    7. ~~help / reference for contrib libraries [#943](https://github.com/processing/processing/issues/943)~~ 
* Done, or awaiting merge 
    * Merged: [PR #2705](https://github.com/processing/processing/pull/2705) 
        * ~~Modes and Tools can now be added, removed and updated without a restart.~~ 
        * ~~In the unlikely chance that this fails to happen without a restart (and this happens only in Windows), a restart button is displayed from which Processing restart automatically.~~ 
        * ~~The tmp folders delete much better, and in case they don't, they are removed the next time Processing is run.~~ 
        * ~~Changes in the UI of the Contribution Managers have been implemented.~~ 
    * ~~Incorrect line coloring when filtering modes list~~ Merged: [PR #2598](https://github.com/processing/processing/pull/2598) 
    * Merged: [PR #2637](https://github.com/processing/processing/pull/2637) 
        * ~~Show installed/available version~~ 
        * ~~post last release date w/ each library in the manager and website~~ 
    * ~~fail more gracefully if no internet connection or a proxy server is in use~~ Merged: [PR #2800](https://github.com/processing/processing/pull/2800) 
    * ~~examples manager needed for books, courses, workshops~~ Merged: [PR #2795](https://github.com/processing/processing/pull/2795)
    * ~~“starred” / “recommended” libraries~~ Merged: [PR #2782](https://github.com/processing/processing/pull/2782).  This was changed to just going to use Processing icon for foundation libraries.
    * ~~different lists for different versions of processing~~ Merged: [PR #2746](https://github.com/processing/processing/pull/2746) 
    * Some smaller fixes to contribution manager: 
        * ~~.properties file gets overwritten with contributions.txt~~ Merged: [PR #2608](https://github.com/processing/processing/pull/2608) 
        * ~~Incorrect mode is selected in mode menu~~ Merged: [PR #2616](https://github.com/processing/processing/pull/2616) 
        * ~~Update manager does not show on startup~~ Merged: [PR #2636](https://github.com/processing/processing/pull/2636) 
        * ~~Status messages don't clear~~ Merged: [PR #2667](https://github.com/processing/processing/pull/2667) 
        * ~~Help>Environment and Help>Reference don't work in Windows~~ Merged: [PR #2657](https://github.com/processing/processing/pull/2657) 
        * ~~contributions managers show specific titles (like "Mode Manager") in the user's preferred language~~ Merged: [PR #2777](https://github.com/processing/processing/pull/2777)
* Awaiting Merge:
    * help / reference for contrib libraries [PR #2804](https://github.com/processing/processing/pull/2804)  
* Post-GSOC Tasks: 
    * Related to the Contributions Manager:
        1. Prompt to install library before running a sketch if not already installed [#2566](https://github.com/processing/processing/issues/2566) 
        2. ProgressMonitor continues to show after an exception is thrown when trying to install a contribution [#2798](https://github.com/processing/processing/issues/2798) 
        3. Reduce scroll amount in Contributions Manager [#2189](https://github.com/processing/processing/issues/2189)
        4. SOCKS proxy not working [2643](https://github.com/processing/processing/issues/2643)
            * the current code that gets/sets the pref is in Preferences
            * instead of current implementation, can we auto-detect proxy settings?
            * old issue: [1476](https://github.com/processing/processing/issues/1476)
            * Info about aetting up a proxy [here](http://www.catonmat.net/blog/linux-socks5-proxy)
            * http://docs.oracle.com/javase/7/docs/technotes/guides/net/proxies.html
            * http://docs.oracle.com/javase/1.5.0/docs/guide/net/proxies.html
            * http://stackoverflow.com/questions/4933677/detecting-windows-ie-proxy-setting-using-java
            * http://www.java2s.com/Code/Java/Network-Protocol/DetectProxySettingsforInternetConnection.htm 
        5. Go through existing tool contributions with Elie (are there outdated tools?) 
        6. Guidelines for modes [#1656](https://github.com/processing/processing/issues/1656) 
    * Auto brackets/quotes closing [processing/processing-experimental#60](https://github.com/processing/processing-experimental/issues/60)
    * REPL in console [processing/processing-experimental#55](https://github.com/processing/processing-experimental/issues/55) : Work underway [here](https://github.com/joelmoniz/REPLmode).

## Gal / Dan
* Tweak mode outstanding issues
    * ~~remove dependency on oscp5 [2730](https://github.com/processing/processing/issues/2730)~~
    * [2799](https://github.com/processing/processing/issues/2799)
* ~~Tweak mode integration [exp#42](https://github.com/processing/processing-experimental/issues/42)~~
    * ~~tweak mode has to be an option (not by default)~~
    * ~~tweak mode will disable editor~~
    * ~~tweak mode will merge into the repo after PDE X does~~
    * ~~Interface process idea:~~
        * ~~Turn on/off tweaking (in Toolbar or Menu)~~
* ~~Java2D PShape should work like P2D [2756](https://github.com/processing/processing/pull/2756)~~
    * [2783](https://github.com/processing/processing/issues/2783)
    * [2784](https://github.com/processing/processing/issues/2784)

## Preprocessor
* Antlr 4?
* using a processing keyword as a variable name gives unhelpful error message [93](https://github.com/processing/processing/issues/93)
* Functions reference for set() need to go to PImage or main set() reference by context
* Started a little collection of issues [here](https://github.com/processing/processing/issues?labels=preprocessor)
  
## Sketchbook
* ~~Pattern Sketchbook after Examples window~~
   * ~~The new Open menu is:~~
       * ~~Open~~
       * ~~Examples~~
       * ~~Sketchbook~~
* ~~Recent (as a list of most recent after a line)~~ (settled on submenu)

## Internationlization
* ~~Language stuff [2173](https://github.com/processing/processing/issues/2173)~~
* ~~Internationalization [632](https://github.com/processing/processing/issues/632)~~

## More
* souped up version of the code folder called “libraries”
* code syntax highlighting (all goes to gray), also [1681](https://github.com/processing/processing/issues/1681)
* undo [707](https://github.com/processing/processing/issues/707)
* auto-format [364](https://github.com/processing/processing/issues/364), [2271](https://github.com/processing/processing/issues/2271)
* `return` keyword not treated as such when followed by a bracket [2099](https://github.com/processing/processing/issues/2099)
* IllegalArgumentException when clicking between editor windows [2530](https://github.com/processing/processing/issues/2530)
* "String index out of range" error [1940](https://github.com/processing/processing/issues/1940)
* closing the color selector makes things freeze (only Linux and Windows?) [2381](https://github.com/processing/processing/issues/2381)
* ~~SOCKS proxy not working [2643](https://github.com/processing/processing/issues/2643)~~
    * ~~the current code that gets/sets the pref is in Preferences~~
    * ~~instead of current implementation, can we auto-detect proxy settings?~~
    * ~~old issue: [1476](https://github.com/processing/processing/issues/1476)~~
    * ~~http://docs.oracle.com/javase/7/docs/technotes/guides/net/proxies.html~~
    * ~~http://docs.oracle.com/javase/1.5.0/docs/guide/net/proxies.html~~
    * ~~http://stackoverflow.com/questions/4933677/detecting-windows-ie-proxy-setting-using-java~~
    * ~~http://www.java2s.com/Code/Java/Network-Protocol/DetectProxySettingsforInternetConnection.htm~~ Moved to Joel's list of post-GSOC work
* problems with non-US keyboards and some shortcuts [2199](https://github.com/processing/processing/issues/2199)

# Saving for later?

## Fantasy PDE X features (we likely won't get to these)
* ~~Auto brackets/quotes closing [exp#60](https://github.com/processing/processing-experimental/issues/60)~~ Moved to Joel's list of post-GSOC work
* Tracing tool? [exp#56](https://github.com/processing/processing-experimental/issues/56)
* ~~REPL in console [exp#55](https://github.com/processing/processing-experimental/issues/55)~~ Moved to Joel's list of post-GSOC work
* Line numbers


## Text Editor
* Try [RTextArea](https://github.com/bobbylight/RSyntaxTextArea) maybe it's actually be worth it, will it fix code syntax highlighting, undo, etc problems?

# Other GSOC

## Imil / Andres
* Command-line jarsign, no programmatic
* add device and sdk selector under Android menu in the PDE: code is in AndroidEditor.java, buildModeMenu() method
* Automatic SDK download: only the SDK default required by Processing (10 or anything newer we update to).
* Manifest editor is low priority

## Levente / Roland / Andres
* Solving low-level issues now
https://github.com/ochafik/nativelibs4java/issues/511
https://github.com/ochafik/nativelibs4java/issues/503
Olivier Chafik (JNAerator) is very happy to help, so we are optimistic about getting the low-level bindings working by the end of next week, following our original schedule. GObject will probably need some manual changes to add all the required API
* Use of JGIR/BridJ to regenerate gstreamer-java seems tricky, but Olivier is willing to help with this as well.
* Ultimately, the high-level gstreamer-java API won’t change much, so it should be fairly straightforward to 
* update the video library to use the new bindings.