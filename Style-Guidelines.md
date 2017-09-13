As the project grows and has more contributors, it's no longer possible to just tell people to “follow the formatting you see in the code.” Then again, that never worked anyway. 

This is an attempt to describe how the source code should be formatted. It's mostly a collection of my notes, but will get better over time as I add to it and organize it further.

## Indentation

Always spaces, two of them. Never tabs.

## Spacing

* Always a space after `if`. Use `if (blah)` not `if(blah)`. Example if/else block:
```
    if (blah) {
      // yes like this
    } else {
      // something besides
    }
```
* No single line `if` blocks
```
if (this) something
else blah blah blah
```
instead use
```
if (this) {
  // something 
} else {
  // blah blah blah
}
```
* No spaces inside parens. 
```
if( blah )  // BAD
if ( blah ){  // BADDER
if (blah) {  // good
```
* Use a space after the paren and before the curly brace: 
```
if (blah) {
``` 
not 
```
if (blah){
```

* An empty block should be `{ }` not `{}` or
```
if (emptyBlock) {
}
```
...unless there's a `//` comment to be made inside the empty block:
```
if (emptyBlock) {
  // a useful comment here about why this case is skipped
}
```

* Use spaces before/after commas:
 * `someFunction(apple,bear,cat); //bad`
 * `someFunction(apple, bear, cat);  // correct`

* Use spaces before/after use of +
 * `String s = "this is an " + "excessive use " + "of quotes to demonstrate concatenation.";`
 * `String s = "this is the "+adjective+" wrong way "+exclamation+" and is tough to read";`


## Brace yourself

Always use braces:
```
for (int i = 0; i < 10; i++) {
  println(i);
}
```
never this:
```
for (int i = 0; i < 10; i++) 
  println(i);
```
Not using braces is too prone to causing subtle errors when merging code from multiple people.

The rare exception is the occasional ‘continue’ statement at the top of a for-loop, or sometimes a single line `if (somethingOrOther) return;` if it just doesn't make sense to have a lot of extras. 

Starting brace goes on same line, end brace goes on its own. An else statement should look like `} else {`

## Blank lines

Use two blank lines between function blocks. 

One blank line after the package declaration. 

Two blank lines between the imports and the class definition.

No blank line after the function definition or before the closing brace.


## Fiddly things

* Use `String[] lines` instead of `String lines[]`

* Only use the `?` operator if it saves multiple lines of code. One probably use is a short function that returns a result immediately, i.e. `return (something == null) ? 0 : Integer.parseInt(something)`

* Place || &&  etc on the end, not the start, of the line. This keeps variables lined up with one another. (This is different from Oracle style)

* `static` goes first (before `public` et al) (This is different from Oracle style)


## Functions 

When adding parameters to a function, add to the end. Don't change order, even if it feels more intuitive for that variation. Only increase the number, don't have alternate forms with the same basic number of arguments.


## Comments

* Always one space after the `//` in single line comments

* Two spaces before `//` at the end of a line (that has code as well)

* Try to use `//` comments inside functions, to make it easier to remove a whole block via `/* */`

* When making a fix related to an issue on Github, include the URL to the issue. Don't just put #3257 or something like that, use the URL. We can spare the extra characters: the extra letters won't make the PDE run slower, but will make it easier for someone returning to the code to look up the issue.

## New lines

* Keep code under 80 columns. Break up statements if you must. 
    * There are some exceptions (the `PreferencesFrame` class, for instance) where breaking things up is even uglier, so the 80 column limit is occasionally ignored.

* Avoid the chaining madness that has afflicted Java programming of late, where dots are placed at the end (or even beginning) of multi-line indented poetry.


## Layout

When I was a young developer, I did crap like this too. Don't be like me:
```
   if (parent ==null) return fromAngle((float)(Math.random()*Math.PI*2),target);
   else               return fromAngle(parent.random(PConstants.TWO_PI),target);
```
(Point being, don't get cute with adding extra space to indentation for symmetry that you like personally. This is really subjective territory, and should just be avoided.)

Don’t stack up declarations and definitions:
```
public static final int STATUS_EMPTY = 100, STATUS_COMPILER_ERR = 200, STATUS_WARNING = 300, STATUS_INFO = 400, STATUS_ERR = 500;
```
Because someday, we're gonna remove STATUS_INFO and that'll make it tougher to see the change. Just write them out:
```
static final int STATUS_EMPTY = 100;
static final int STATUS_COMPILER_ERR = 200;
...etc
```

If importing many items inside a single package, consider using * instead of listing out a dozen individual classes.

Please do not expand the imports in source that you’re editing. 

Where possible, make sure text files checked into the repo are text files, and are marked as such so they can use the correct encoding for the platform. Right now, we’re not doing this consistently in the repo, but please use this convention for newer files (or help us fix the others).


## Copyrights and Attribution

* Copyright will be assigned to [The Processing Foundation](http://foundation.processing.org/). This is our non-profit entity that supports the work. If you don't want to assign copyright, you cannot contribute. If you *cannot* assign copyright (meaning that it's not your code, it's another license, etc), then *do not* contribute.

* Skip the bylines on source. Your code will be reworked so much by the time it's actually used that it just doesn't make sense. The commit history will tell a more accurate story anyway.


## Philosophical

* **Inner classes** don’t reach in and reference inner classes from classes not in the same file.

* **GUI code** As much as possible, GUI code should not live inside `processing.app.Base`. we rely on `processing.app.Toolkit` for that. This keeps the command line versions behaving better.

* **Ordering if blocks** Where possible make the default case the first part of the ‘if’ block. this can’t be done slavishly because it can make things awkward, but it’s generally a useful idea.

* **Already commented code** There are many commented-out sections of code. Moreso than is actually a good idea. Usually they’re the result of trying many different things before getting to a final/working solution. It also sometimes prevents me from going back and making the same mistake again. This is, of course, bad practice: The former should be fixed with documentation, the latter fixed by heavier reliance on the version control system. However, since one developer is doing the vast majority of the work, I don’t win style points by cleaning up code for people who want to peruse it—and it takes time away if I have to come back and finish debugging a feature (I'm a bit feeble-minded that way). Because development is sporadic, I often have to set something down before it's finished, so I keep the alternate bits around. Also, it's often the case that one version of the code works on one platform (or version of Java) and not another. These go in and out of testing as I move around between platforms.