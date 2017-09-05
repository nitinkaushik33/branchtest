To develop a tool for Processing, the [Eclipse Tool Template](https://github.com/processing/processing-templates/wiki/Eclipse-Tool-Template) project provides an Eclipse template.

Please inform us about the existence of your tool by posting your contribution to the forum in the [Libraries and Tool Development](http://forum.processing.org/library-and-tool-development) topic. Be sure to let us know where we can find the tool's web page online.

Each tool contribution should include the following:

* Online summary page. A Processing tool should have its own web page, stored at a stable URL, and should include:
  1. A short abstract that describes the purpose of the tool. A screenshot is encouraged if the tool uses any external editor windows.
  1. The tool has been successfully tested on which platforms?
  1. The latest Processing version the tool has been tested with?
  1. Source code. We recommend using an online service such as GitHub or Google Code to host the source code, then it is very easy to browse the code online.
  1. Keywords that describe the aim and function of the tool.
  1. Last update. When was the last update of the tool?
  1. A link to a zip file that includes the tool
* Source. We strongly encourage you to open source your tool. If you don't want to distribute source, that's perfectly fine, however only tools that include their code will be promoted at [processing.org/reference/tools](http://processing.org/reference/tools). We're giving away all our stuff, and we want others to do so as well because it's good for the community. This also ensures that your tool lives on past your own interest in its maintenance.

Your online summary page can be the URL of the site that hosts your source if that site can accommodate the information above. Documentation for contributed tools outside the previous list is not crucial. However, given we encourage you to release your tools' source (see below), it would make sense that your code is well commented so that it may serve as a reference for aspiring tool developers.

## Folder Structure
Tools should be distributed as zipped files, and the distribution should be laid out as follows:

* `theTool/tool/theTool.jar`
* `theTool/src/`
* `theTool/tool.properties`

The `tool` folder contains the tool's JAR file (and if necessary, any additional `.jar`, `.dll`, `.so`, or `.jnilib` files). The name of the outermost folder must conform to the name of the class implementing the Tool interface. The name of the jar contained in `tool` does not matter. See the page on [[Tool Basics|Tool-Basics]] for more information.