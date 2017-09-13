We've put a huge amount of work into making it possible for Processing 3 to run in multiple languages. 

This has been an exciting improvement, and it's been great to see all the help from the community, which has provided several new languages and continued to refine them. Join us and contribute!

## Two ways to get started

If you'd like to help the community by adding a new language or improving an existing translation, there are two options: 

* You can [build the code](https://github.com/processing/processing/wiki/Build-Instructions) and modify the `.properties` files inside `processing/build/shared/lib/languages` to add or modify an existing language. When you have updates, submit a [pull request](https://github.com/processing/processing/wiki/Contributing-to-Processing-with-Pull-Requests) with the updates.

* If you're not comfortable with building from source, simply make a folder called `languages` inside your sketchbook. Then copy one of the existing `.properties` files from your Processing download, and edit away. You'll probably need to restart Processing to see the changes. 

## Translating Processing to a new language

If you are translating to a new language, there are a couple of things you will need to setup first before it works.

 * Copy the default translation at `build/shared/lib/languages/PDE.properties` to `build/shared/lib/languages/PDE_xx.properties` where `xx` is the Java code for your language (usually the ISO 639-1 code).
 * Add your new language code to the `build/shared/lib/languages/languages.txt` file.
 * Translate strings in the file you just copied (change only the text after the `=` sign)
 * Rebuild the project and restart Processing to see the changes

## Improving an existing translation

To find missing strings in an existing translation, you can use [this script](https://gist.github.com/federicobond/741d5c7df61191e13408).

Download it to the root of your Processing source code and make it executable:

````
curl https://gist.githubusercontent.com/federicobond/741d5c7df61191e13408/raw/d8862f2599fd26ba88833094548d4bd77a8f6b5f/missing.sh > missing.sh
chmod +x ./missing.sh
````

If you call it like this:

````
./missing.sh
````

It will show strings that are missing from the default English properties file (indented lines are those found in the .properties file but not in the codebase)

If you call it with a language code as an argument:

````
./missing.sh es
````

It will compare the keys for that language against the keys in the default language .properties file. Again, the behavior with regards to indented lines is similar: those lines appear in the corresponding language file but were removed from the default one.

You can get false positives occasionally from this tool, depending on how the actual code is split into lines. Be sure to check for usages in the source code before removing or renaming any obsolete key.
