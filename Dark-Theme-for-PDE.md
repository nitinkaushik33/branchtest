Programmers sometimes prefer to code on a dark background with light text when working late at night or in low-light conditions in order to avoid eye strain.

## Invert all colors on your computer

Many operating systems have a system-wide setting that will invert colors on all applications, turning white editors dark and dark text light. For example:

1. OS X: System Preferences > Accessibility > Display > Invert Color
2. Windows 7: Magifier > Preferences > Turn on color inversion
3. Linux: in a terminal type `xrandr --output DP1 --brightness -1` (where `DP1` is your current display, and `-1` means inverted colors, `1` means normal)

## Change PDE colors only

There are two Processing files that you should edit:

1. preferences.txt
2. lib/theme.txt

Many colors can be adjusted, but here is a simple example.

Close Processing before editing the files.

### theme.txt

This file defines colors for the IDE. Find and change these three values (the default text color to bright gray, background color to dark gray and current line highlight color to mid gray):

```
editor.fgcolor = #eeeeee
editor.bgcolor = #222222
editor.linehighlight.color=#555555
```

### preferences.txt

This file contains the colors for syntax highlighting. Replace all lines that contain `editor.token`:

```
editor.token.comment1.style=#999999,plain
editor.token.comment2.style=#999999,plain
editor.token.function1.style=#ffff00,plain
editor.token.function2.style=#ffff00,plain
editor.token.function3.style=#669900,plain
editor.token.function4.style=#ffff00,bold
editor.token.invalid.style=#999999,bold
editor.token.keyword1.style=#33997e,plain
editor.token.keyword2.style=#33997e,plain
editor.token.keyword3.style=#669900,plain
editor.token.keyword4.style=#d94a7a,plain
editor.token.keyword5.style=#e2661a,plain
editor.token.keyword6.style=#33997e,plain
editor.token.label.style=#999999,bold
editor.token.literal1.style=#00ffff,plain
editor.token.literal2.style=#718a62,plain
editor.token.operator.style=#6699,plain
```

Restart Processing to see the effect.