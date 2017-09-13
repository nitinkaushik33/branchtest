An example package is a set of sample Processing sketches bundled together that can be downloaded and installed so the user can access them from the Processing Examples window. A group of examples for a book, class, website, etc. can be grouped and formatted to make use of this new feature.
  
## Creating an Examples Contribution 
  
An Examples contribution is a set of working processing sketches organized into folders. The exact folder structure is  described below.  
  
### Folder Structure  
  
Examples contributions should be distributed as zipped files with the following required structure:  
  
```
ExamplesPackage/examples/
ExamplesPackage/examples.properties
```  
  
Here, the sub-directory ```examples``` contains the example sketches (which may or may not be organized in directories, as required). The ```examples.properties``` file is used to describe the Examples contribution, as described in the next sub-section.
  
### Describing the Examples Contribution -- examples.properties  
  
Like the .properties file of other contributions, the examples.properties file provides the details to the Examples Manager (which is used to install and remove Examples contributions).
  
The basic fields to be included in the .properties file, along with an illustration and description of each field, are shown below:

```
# UTF-8 supported.

# The name of your examples-package as you want it formatted.
name = My Processing Examples

# List of authors. Links can be provided using the syntax [author name](url).
authorList = [Author One](http://www.authorone.com/) and [Author Two](http://authortwo.com/)

# A web page for your examples-package, NOT a direct link to where to download it.
url = http://www.myp5examples.com/

# The category of your examples-package, must be one (or many) of the following:
#   "3D"            "Animation"     "Compilations"      "Data"          
#   "Fabrication"   "Geometry"      "GUI"               "Hardware"      
#   "I/O"           "Language"      "Math"              "Simulation"    
#   "Sound"         "Utilities"     "Typography"        "Video & Vision"
# 
# If a value other than those listed is used, your examples-package will listed as 
# "Other".
category = Geometry

# A short sentence (or fragment) to summarize the examples-package's function. This will 
# be shown from inside the PDE when the examples-package is being installed. Avoid 
# repeating the name of your examples-package here. Also, avoid saying anything redundant 
# like mentioning that it's an examples-package. This should start with a capitalized 
# letter, and end with a period.
sentence = A set of sketches demonstrating the creation of complex geometric shapes.

# Additional information suitable for the Processing website. The value of
# 'sentence' always will be prepended, so you should start by writing the
# second sentence here. If your examples-package only works on certain operating systems,
# mention it here.
paragraph =  

# Links in the 'sentence' and 'paragraph' attributes can be inserted using the
# same syntax as for authors. 
# That is, [here is a link to Processing](http://processing.org/)

# A version number that increments once with each release. This is used to 
# compare different versions of the same examples-package, and check if an update is 
# available. You should think of it as a counter, counting the total number of 
# releases you've had.
version = 2  # This must be parsable as an int

# The version as the user will see it. If blank, the version attribute will be 
# used here.
prettyVersion = 1.20  # This is treated as a String

# The min and max revision of Processing compatible with your examples-package.
# Note that these fields use the revision and not the version of Processing, 
# parsable as an int. For example, the revision number for 2.2.1 is 227. 
# You can find the revision numbers in the change log: 
# https://raw.githubusercontent.com/processing/processing/master/build/shared/revisions.txt
# Only use maxRevision (or minRevision), when your examples-package is known to 
# break in a later (or earlier) release. Otherwise, use the default value 0.
minRevision = 0
maxRevision = 227

# The list of modes that the examples-package is compatible with. This basically 
# affects when the examples-package is listed in the Examples tree once installed 
# (although this does not affect when the examples-package is displayed/greyed-out in 
# the Examples Contributions Manager). This is to be provided as a list of fully qualified 
# classnames of the mode that the examples-package is compatible with (as can be obtained 
# from mode.id in the sketch.properties file). Leaving this blank will assume that 
# the examples-package is compatible with all modes.
compatibleModesList = de.bezier.mode.coffeescript.CoffeeScriptMode, processing.mode.java.JavaMode
```

## Advertising Your Examples

Starting with Processing 3.0, example packages are a part of the Processing Development Environment (PDE). To be included in the list in the PDE, you'll need to include a `examples.properties` file with your examples zip and make a few changes to how it's hosted on your server.

First, you must include the following attributes in `examples.properties`: 
* `name`
* `authorList`
* `url`
* `category`
* `sentence`
* `version`

You should also set the `minRevision` and `maxRevision` attributes to indicate the Processing revisions compatible with your library. Note that these fields use the [revision](https://raw.githubusercontent.com/processing/processing/master/build/shared/revisions.txt) and not the version of Processing (e.g. the revision number for 2.2.1 is 227). Only use `maxRevision` (or `minRevision`), when your library is known to break in a later (or earlier) release. Otherwise, use the default value `0`.

You will need to provide a static link to the latest version of your library, and host a copy of your `examples.properties` alongside it. The result on your server should look something like this:

```
http://www.example.com/awesomeExamples.zip (The latest version of awesomeExamples)
http://www.example.com/awesomeExamples.txt (A copy of the library.properties file contained in awesomeExamples.zip)
```

Once everything is in place, send your static links to the Processing Librarian: [Elie Zananiri](mailto:prisonerjohn+p5@gmail.com). We'll review your properties file to make sure everything is in order and add your contribution to the list.

On our end, we'll only record the location of `awesomeExamples.txt`, and we'll assume that a copy of the library file is hosted at an address by the same name, except ending in `zip`. Each day, a script on processing.org will scrape the information from all the .txt files and aggregate it into a single file, which is then used by each user to browse what's available and check for updates.

## Releasing An Update

When you want to release a new version of your library, here's what you'll need to do:

1. Update your `examples.properties` file inside your `.zip`
  * Increment the value of `version`. This is an integer that we'll use to check for updates. You can think of it as a counter, counting the total number of releases you've had.
  * Write whatever you want for the new value of `prettyVersion`.
1. Copy your latest release to the static address you gave us earlier (e.g. http://www.example.com/awesomeExamples.zip)
1. Copy the `examples.properties` file from your latest release to a `.txt` file hosted at an address by the same name as your `.zip`, except instead ending in `.txt` (e.g. [Examples.txt](https://onlineessay.us/)