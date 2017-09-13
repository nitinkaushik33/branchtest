Tools allow Processing users to modify or extend the Processing Development Environment (PDE). If you've ever used the Auto Format, Create Font, or Color Selector features, you've used a tool. Tools like these come standard with Processing, but as of release 0147, developers can add their own tools to the Tools menu.

Tools can interact directly with the [`Editor`](https://github.com/processing/processing/blob/master/app/src/processing/app/Editor.java) object responsible for rendering the PDE's main editor panel. Tool developers can poll the Editor object for data such as the user's selection or caret position. The `Editor` object can also be used to modify sketch contents or display a message in the status bar.

You may also use `PApplet` or another GUI library (such as Java's Swing) to create additional editor windows such as the Color Selector. These interfaces might be used to insert code into the sketch or manipulate data in the sketch folder.

## Where to Put Tools

Tools that come with Processing are inside the `tools` subfolder of the Processing distribution, but tools you download and install yourself should be placed inside your Processing sketchbook folder, inside a folder named `tools`. (If you have an older version of Processing, the `tools` folder might not exist. If it's not there, you'll need to create it; make sure it's called `tools` and not `tool`).

## Build Your Own Tool
If you are building your own tool, the [Eclipse Tool Template](https://github.com/processing/processing-tool-template) will help you to get started developing your tool with Eclipse. The [[Tool Basics|Tool-Basics]] page will give you a better understanding of how a tool works. If you want to share your tool with the processing community, please take a look at the [[Tool Guidelines|Tool-Guidelines]].

It's not possible to build tools from within the Processing application. Like libraries, **creating a tool with the PDE will cause problems** because the JAR file exported from the PDE will contain the current version of the `processing.core` classes, which will cause major conflicts when trying to use the PDE. Tools that contain `processing` packages in this manner will have to be rejected or removed from the site.

The Processing Development Environment is built with the sole purpose of creating sketches that are part of `PApplet` that have a few files at most. We don't plan to extend the PDE to also support developing libraries or tools, because then it becomes like any other IDE that is quickly too general for our target audience. Users who are advanced enough in their programming skills to build tools will almost always be skilled enough to use another IDE like Eclipse to build their tool. (And if not, it's a lovely time to learn.)

## Core vs. Contributed Tools

There are two categories of tools. The core tools (Auto Format, Color Selector, Create Font) are part of the Processing distribution, and contributed tools are developed, owned, and maintained by members of the Processing community.

Tools make the Processing Development Environment more powerful and extensible. A few contributed libraries have become part of Processing's core distribution and we can assume that tools of equal quality and general purpose may be incorporated into Processing's default set of tools.