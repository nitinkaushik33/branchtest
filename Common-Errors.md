unexpected token: something
---------------------------

**Translation: I’m expecting a piece of code here that you forgot, most
likely some punctuation, like a semi-colon, parentheses, curly bracket,
etc.**

This error is pretty much always caused by a typo. Unfortunately, where
the error points you to can be misleading. The “something” is sometimes
just fine and the actual error is caused by the line before or after
that piece of code. Anytime you forget or include an improper comma,
semi-colon, quote, parentheses, bracket, etc., you’ll get this error.
Here are some examples:

Incorrect:

``` {.processing}
int val = 5
```

Correct:

``` {.processing}
int val = 5; 
```

Found one too many { characters without a } to match it
-------------------------------------------------------

**Translation: You forgot to close a block of code, such as an if
statement, a loop, a function, a class, etc.**

Incorrect:

``` {.processing}
void setup() {
  for (int i = 0; i < 10; i++) {
    if (i > 5) {
      line(0,i,i,0);
      println("i is greater than 5");  
  }  
}
```

Correct:

``` {.processing}
void setup() {
  for (int i = 0; i < 10; i++) {
    if (i > 5) {
      line(0,i,i,0);
      println("i is greater than 5");
    }  
  }  
}
```

No accessible field named "myVar" was found in type "Temporary\_7665\_1082”
---------------------------------------------------------------------------

**Translation: I don’t know about the variable “myVar.” It’s not
declared anywhere I can see.**

This error will happen first and foremost if you simply don’t declare a
variable. Remember, you can’t use a variable until you’ve said what type
it should be. You’ll get the error if you write:

``` {.processing}
myVar = 10;
```

instead of:

``` {.processing}
int myVar = 10;
```

This error can also occur if you try to use a local variable outside of
the block of code where it was declared. For example:

``` {.processing}
if (mousePressed) {
  int myVar = 10; 
}
ellipse(myVar,10,10,10); // ERROR! myVar is local to the if statement so it cannot be accessed here.
```

Here’s a corrected version:

``` {.processing}
int myVar = 0;
if (mousePressed) {
  myVar = 10; 
}
ellipse(myVar,10,10,10); // OK!  The variable is declared outside of the if statement.
```

Or if you’ve declared a variable in setup(), but try to use it in
draw().

``` {.processing}
void setup() {
  int myVar = 10;  
}

void draw() {
  ellipse(myVar,10,10,10);  // ERROR! myVar is local to the setup() so it cannot be accessed here.
}

int myVar = 0;  // Corrected, declared as global!

void setup() {
  myVar = 10;
}

void draw() {
  ellipse(myVar,10,10,10);
}
```

The same error will occur if you use an array in any of the above
scenarios.

``` {.processing}
myArray[0] = 10; // ERROR!  No array was declared.
```

The variable "myVar" may be accessed here before having been definitely assigned a value
----------------------------------------------------------------------------------------

**Translation: You declared the variable “myVar”, but you did not
initialized it. You should give it a value first.**

This is a pretty simple error to fix. Most likely, you just forgot to
give your variable its default starting value. This error only occurs
for local variables (with global variables Processing will either not
care, and assume the value is zero, or else give throw a
NullPointerException (see later).

``` {.processing}
int myVar;          // Error myVar doesn't have a value!
line(0, myVar,0,0);

int myVar = 10;     // Corrected!
line(0, myVar,0,0);
```

This error can also occur if you try to use an array before allocating
its size properly.

``` {.processing}
int[] myArray;      // ERROR!  myArray was not created properly.
myArray[0] = 10;

int[] myArray = new int[3];  // OK!  myArray is an array of three integers.
myArray[0] = 10;
```

java.lang.NullPointerException
------------------------------

**Translation: I’ve encountered a variable whose value is null. I can’t
work with this.**

The NullPointerException error can be one of the most difficult errors
to fix. It is most commonly caused by forgetting to initialize an object
with the constructor. When you declare a variable that is an object, it
is first given the value of null, meaning nothing. (This does not apply
to primitives, such as integers and floats.) If you attempt to then use
that variable without having initialized it (for example, by calling one
of its methods), this error will occur. Here are a few examples (that
assume the existence of a class called “Thing”).

``` {.processing}
Thing thing;
void setup() {

}

void draw() {
  thing.display();  // ERROR!  “thing” was never initialized and therefore has the value null.
}
```

Corrected:

``` {.processing}
Thing thing;
void setup() {
  thing = new Thing(); 
}

void draw() {
  thing.display();  // OK!  “thing” is not null because it was initialized in setup().
}
```

Sometimes, the same error can occur if you do initialize the object, but
do so as a local variable by accident.

``` {.processing}
Thing thing;
void setup() {
  Thing thing = new Thing();  // ERROR!  This line of code declares and initializes a different “thing” variable (even though it has the same name.)  
                              // It is a local variable for only setup().  The global “thing” is still null!!
}

void draw() {
  thing.display();
}
```

The same goes for an array as well, if you forget to initialize the
elements, you’ll get this error.

``` {.processing}
Thing[] things = new Thing[10];
for (int i = 0; i < things.length; i++) {
   things[i].display();   // ERROR! All the elements on the array are null!
}
```

Corrected:

``` {.processing}
Thing[] things = new Thing[10];
for (int i = 0; i < things.length; i++) {
  things[i] = new Thing(); 
}
for (int i = 0; i < things.length; i++) {
  things[i].display();  // OK! The first loop initialized the elements of the array.
}
```

Finally, if you forget to allocate space for an array, you can also end
up with this error.

``` {.processing}
int[] myArray;

void setup() {
  myArray[0] = 5;   // ERROR!  myArray is null because you never created it and gave it a size.
}
```

Corrected:

``` {.processing}
int[] myArray = new int[3];

void setup() {
  myArray[0] = 5;   // OK!  myArray is an array of three integers.
}
```

Type "Thing" was not found
--------------------------

**Translation: You are trying to declare a variable of type Thing, but I
don’t know what a Thing is.**

This error occurs because you either (a) forgot to define a class called
“Thing” or (b) made a type in the variable type.

A typo is pretty common:

``` {.processing}
intt myVar = 10;  // ERROR!  You probably meant to type “int” not “intt.”
```

Or maybe you want to create an object of type Thing.

``` {.processing}
Thing myThing = new Thing();  // ERROR!  If you didn’t declare a class called “Thing.”
```

This will work, of course, if you write:

``` {.processing}
void setup() {
  Thing myThing = new Thing(); // OK!  You did declare a class called “Thing.”
}

class Thing {
  Thing() {
  }
}
```

Finally, the error will also occur if you try to use an object from a
library, but forget to import the library.

``` {.processing}
Capture video;  // ERROR!  You forgot to import the video library.
void setup() {
  video = new Capture(this,320,240,30);  
}
```

Corrected:

``` {.processing}
import processing.video.*;

Capture video;  // OK!  You imported the library.
void setup() {
  video = new Capture(this,320,240,30); 
}
```

Perhaps you wanted the overloaded version "type function(type \$1, type \$2, . . .);" instead?
----------------------------------------------------------------------------------------------

**Translation: You are calling a function incorrectly, but I think I
know what you mean to say. Did you want call this function with these
arguments?**

This error occurs most often when you call a function with the incorrect
number of arguments. For example, to draw an ellipse, you need an x
location, y location, width, and height. But if you write:

``` {.processing}
ellipse(100,100,50);    // ERROR!  ellipse() requires 4 arguments.
```

You’ll get the error: “Perhaps you wanted the overloaded version "void
ellipse(float \$1, float \$2, float \$3, float \$4);" instead?” The
error lists the function definition for you, indicating you need four
arguments, all of floating point. The same error will also occur if you
have the right number of arguments, but the wrong type.

``` {.processing}
ellipse(100,100,50,"Wrong Type of Argument");   // ERROR!  ellipse() can not take a String!
```

“No method named "fnction" was found in type "Temporary\_9938\_7597". However, there is an accessible method "function" whose name closely matches the name "fnction"
----------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Translation: You are calling a function I’ve never heard of, however,
I think I know what you want to say since there is a function I have
heard of that is really similar.**

This is a similar error and pretty much only happens when you make a
typo in a function’s name.

``` {.processing}
elipse(100,100,50,50);  // ERROR!  You’ve got the right number of arguments, but you spelled “ellipse” incorrectly.
```

No accessible method with signature "function(type, type, . . .)" was found in type "Temporary\_3018\_2848"
-----------------------------------------------------------------------------------------------------------

**Translation: You are calling a function that I’ve never heard of. I
have no idea what you are talking about!**

This error occurs if you call a function that just plain doesn’t exit,
and Processing can’t make any guess as to what you meant to say.

``` {.processing}
functionCompletelyMadeUp(200);  // ERROR!  Unless you’ve defined this function, Processing has no way of knowing what it is.
```

Same goes for a function that is called on an object.

``` {.processing}
Capture video = new Capture(this,320,240,30);
video.turnPurple();   // ERROR!  There is no function called turnPurple() in the Capture class. 
```

java.lang.ArrayIndexOutOfBoundsException: \#\#
----------------------------------------------

**Translation: You tried to access an element of an array that doesn’t
exist.**

This error will when the index value of any array is invalid. For
example, if your array is of length ten, the only valid indices are zero
through nine. Anything less than zero or greater than nine will produce
this error.

``` {.processing}
int[] myArray = new int[10];

myArray[-1] = 0;   // ERROR!  -1 is not a valid index.
myArray[0] = 0;
myArray[5] = 0;
myArray[10] =  0;  // ERROR!  10 is not a valid index.
myArray[20] = 0;   // ERROR!  20 is not a valid index.
```

This error can be a bit harder to debug when you are using a variable
for the index.

``` {.processing}
int[] myArray = new int[100];
myArray[mouseX] = 0;  // ERROR!  mouseX could be bigger than 99.

int index = constrain(mouseX,0,myArray.length-1);  // OK!  mouseX is constrained between 0 and 99 first.
myArray[index] = 0;
```

A loop can also be the source of the problem.

``` {.processing}
for (int i = 0; i < 200; i++) {
   myArray[i] = 0;  // ERROR!  i loops past 99.
}

for (int i = 0; i < myArray.length; i++) {
   myArray[i] = 0;  // OK!  Using the length property of the array as the exit condition for the loop.
}

for (int i = 0; i < 200; i++) {
  if (i < myArray.length) {
    myArray[i] = 0;  // OK!  If your loop really needs to go to 200, then you could build in an if statement inside the loop.
  }
}
```
