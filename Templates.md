Starting with Processing 3.2, a `templates` directory has been added to the sketchbook. If you'd like to have a standard set of code that shows up every time you create a new sketch, you can add files there. 

You can have one template per Mode. To set your default template for Java Mode, for instance, create a directory called `Java` inside the `templates` directory in your sketchbook. Inside that `Java` directory, create a file called `sketch.pde`. Next time you create a new sketch, all files from the `Java` directory will be copied to your new sketch, and the `sketch.pde` file will be used to create *yoursketchname*.pde. 

If the Mode you're using has its own template, your own template will always override it. 

There are no plans to support more than one template per Mode. This would be better handled by a [Contributed Tool](https://github.com/processing/processing/wiki/Tool-Basics) and customized to your heart's content.

Mode authors can create a `template` directory and its contents will automatically be copied the same way.

