## Why

Processing has been around a while, and it's gotten large and complex enough that managing it all in a single repository became unwieldy.  By spreading different portions of the source across multiple repos, we introduce some organizational complexity with the benefit (hopefully) that individual contributors maintain their sanity with logically grouped collections of code.

If you want to contribute to the project (by logging issues or submitting pull requests), it's important to understand how these repos are organized.

This page lists all the Processing repos, and explains what they contain and how they interact.

## Where

All official repos are owned by the Processing organization account:

[**https://github.com/processing**](https://github.com/processing)

Repositories are as follows.  When logging issues, *please* log them to the most relevant repo.

[https://github.com/processing/**processing**](https://github.com/processing/processing)  
The primary repo, containing the core of the Java-based IDE and the Processing API.

[https://github.com/processing/**processing-docs**](https://github.com/processing/processing-docs)  
All files pertaining to the reference documentation, the website, and built-in examples live here, as they share a lot of information.  For example, the "Reference" area that is built in to the IDE also gets published to the website, but so is information about Libraries, as are many of the built-in examples.  We have fancy scripts that extract and repackage all this information in different forms – once for the application, and once for the site.

That said, some information on the reference pages are pulled directly from the Java source in the **processing/processing** repo.  Pull up [a sample reference page](http://processing.org/reference/fill_.html) and note that while the first two elements live in XML files in **processing-docs**…

- Examples
- Description

…the additional information is extracted directly from the Java source:

- Syntax
- Parameters
- Returns
- Related

When we run the reference build script, these information sources are merged, and everything is tied up with a pretty bow on top.  (The latter elements above are also pulled into the auto-generated [JavaDoc](http://processing.org/reference/javadoc/core/), of course.)  This is important because submitting or proposing changes to the reference may involve edits to both **processing/processing** and **processing/processing-docs**.

This repo used to be called **processing-web**, but that has been archived and retired.

[https://github.com/processing/**processing-video**](https://github.com/processing/processing-video)  
Contains everything for the built-in Video library.  This used to be part of **processing/processing**, but it was so large that we moved it out to its own repo.

[https://github.com/processing/**processing-sound**](https://github.com/processing/processing-sound)  
Contains everything for the built-in Sound library.  This used to be part of **processing/processing**, but it was so large that we moved it out to its own repo.

[https://github.com/processing/**processing-android**](https://github.com/processing/processing-android)  
Everything related to the Android mode.

[https://github.com/processing/**processing-library-template**](https://github.com/processing/processing-library-template)  
The template for building and generating your own Processing library.

[https://github.com/processing/**processing-forum**](https://github.com/processing/processing-library-forum)  
All the code behind the lovely, lively, and useful [forum](http://forum.processing.org/two/).

**p5.js** is maintained separately, and has [its own repositories](https://github.com/processing/p5.js/wiki/Development#repositories).

## Other Repos…

…not owned by the Processing organization account:

[https://github.com/jdf/processing.py](https://github.com/jdf/processing.py)  
Python Mode for Processing source.

[https://github.com/kazimuth/processing-py-site](https://github.com/kazimuth/processing-py-site)  
Source for the Python Mode’s documentation and website, [py.processing.org](http://py.processing.org)