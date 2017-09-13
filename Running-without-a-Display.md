Let's say you want to run a Processing sketch on a server. Like maybe you want to generate [several million PDF and JPEG images](http://fathom.info/yearinnikefuel) using a handful of [Amazon EC2](http://aws.amazon.com/ec2) instances. This is called “headless” mode, and to do so, it's necessary to install what's known as a virtual frame buffer. 

(Note, this is unlikely to work on a Raspberry Pi, though [these instructions](https://nocduro.ca/2016/01/06/running-an-exported-processing-3-sketch-on-a-headless-raspberry-pi/) may help.)

### Install Required Libraries  

On Ubuntu 14.04, these are the things you need to install first:
```
sudo apt-get install xvfb libxrender1 libxtst6 libxi6 
```

We'll also assume that Java is already installed – if not you'll need to do something like:

```
sudo apt-get install default-jdk
```

You don't actually need the JDK to run the sketch so this is also ok:

```
sudo apt-get install default-jre
```

Make sure you do not specify a "headless" Java (for example `openjdk-7-jre-headless`), as it won't work with the suggestions below.


### Option 1: Easiest

Using `xvfb-run`, which is installed in the step above, we can run a Java program (like a Processing sketch) from inside a virtual window server, without the messy details in Option #2. Simply run your sketch with the `xvfb-run` command in front of it:

```
xvfb-run /home/<username>/processing/processing-java --sketch=/path/to/sketch/folder --run
```
It might give you a warning about not being able to parse a display, but it should still launch ok.

### Option 2: Harder, But More Control  

If Option #1 above doesn't work or you want more control, you can try making a fake "virtual display" that Processing can use:

```
sudo Xvfb :1 -screen 0 1024x768x24 </dev/null &
export DISPLAY=":1"
```

Then, run a sketch as usual from the command line:

```
/home/<username>/processing/processing-java --sketch=/path/to/sketch/folder --run
```

Or one that has been exported as a Linux application from the PDE.

### Why Do I Need To Do This? 

It's necessary to use the virtual frame buffer because it would require a truly ridiculous amount of work to make Processing so general that it could be done without a display. This would involve a great deal of code and abstraction that simply doesn't make sense when 99.9999% of the code created with Processing will be run with a display. Happily, this method works well and prevents us from needing to double the size of `PApplet`.


### Headless Java Command

Another option is to mess with the command line parameters that launch Java. If you add `-Djava.awt.headless=true` to the line that runs the `java` command, that may be all you need. Read more about Java's Headless Mode [here](http://www.oracle.com/technetwork/articles/javase/headless-136834.html). For most cases, this is less likely to work, but may provide clues for how to get a more complicated sketch running on your machine.