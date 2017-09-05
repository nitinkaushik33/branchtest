To develop a library for Processing, the [Eclipse Library Template](https://github.com/processing/processing-templates/wiki/Eclipse-Library-Template) project provides an Eclipse template.

Please inform us about the existence of your library by posting your contribution in the Processing Forum under [Create & Announce Libraries](http://forum.processing.org/two/categories/create-announce-libraries). Be sure to let us know where we can find the library's web page online.

Each library contribution should include the following:
* Documentation. We recommend using Javadoc-style comments in your library code since it is the most common way to document a Java API. You can use Sun's Javadoc tool to create documentation, or any number of other tools that can convert code with Javadoc-style comments into lovely documentation. The documentation should be stored in a folder named "reference", and include an index.html file that is the starting point.
* Examples. Users tend to learn best from examples, therefore examples are important for a library release. It is highly recommended to support your library with various sample programs to demonstrate the use and potential of the library.
* Properties file. To show information about your library from within the PDE, you need to provide a `library.properties` file. This file contains the full name of your library, a brief summary of its purpose, and other information. More information on the [[Library Basics|Library-Basics#wiki-DescribingYourLibrary]] page.
* Online summary page. A Processing library should have its own web page, stored at a stable URL (or at least as stable as possible), and should include:
  1. A short abstract that describes the purpose of the library.
  1. The library has been successfully tested on which platforms? (OS X, Windows XP and Vista, Linux)
  1. The latest Processing version the library has been tested with?
  1. Dependencies. Does the library depend on any other library?
  1. A list of examples that demonstrate the use and potential of the library.
  1. Source code (if open source). We recommend using Google Code to host the source code of a library in a SVN repository, then it is very easy to browse the code online.
  1. Keywords that describe the aim and function of the library.
  1. Last update. When was the last update of the library?
  1. A link to a zip file that includes the library, documentation and examples.
* Source. We strongly encourage (and will soon require as a stipulation for placement on the site) that the source to your library be included. If you don't want to distribute source, that's perfectly fine, however only libraries that include their code will be promoted at [processing.org/reference/libraries](http://processing.org/reference/libraries). We're giving away all our stuff, and we want others to do so as well because it's good for the community. This also ensures that your library lives on past your own interest in its maintenance.

## Folder Structure

Libraries should be distributed as zipped files, and the distribution should be laid out as follows:
* `theLibrary/library/theLibrary.jar`
* `theLibrary/reference/`
* `theLibrary/examples/`
* `theLibrary/src/`
* `theLibrary/library.properties`

The `reference` folder contains the documentation in HTML format as generated from Javadoc, the `examples` folder contains a set of sketches that help to understand the usage and functionality of the library. The `library` only contains the library's JAR file (and if necessary, any additional `.jar`, `.dll`, `.so`, or `.jnilib` files). Anything that is found inside the `library` folder will be exported with your sketch. The `src` folder contains the source. The name "src" is used because that's the default for Eclipse (and presumably other IDEs).

Following the folder structure is important because it simplifies documentation, and makes it easier for users to know what to expect. It also means that your reference pages can automatically be added to the Help menu in the PDE, and your library examples will automatically be added to the Examples menu. By placing your library in a `.zip` file and following the structure above, it enables future possibilities for automatic installation and library updates.

### A note for Mac OS X users:
Be sure to remove `.DS_Store` files created by Mac OS X from the folders before posting. The following command can be executed in `Terminal.app` to delete all `.DS_Store` files (recursively) from a folder:
```
find YourFolderName -name .DS_Store -ls -exec rm {} \; 
```
Be careful to specify your folder name properly. Don't use `/` or something that would cause the very powerful, very efficient `find` command to remove all `.DS_Store` files from your disk.

Or create directly a `.zip` file without `.DS_Store` files:
```
zip -r theLibrary.zip theLibrary -x "*.DS_Store"
```