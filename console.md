---
title: Console
layout: default
---

## Using the Neko Console

Neko comes with an interactive interpreter, which may be invoked via `nekoc -c`

You may then type in as much code as you would like, then execute it by ending a line (may be otherwise empty) with an exclamation point (`!`).

For example:

    > $print("Hello\n") !
    Hello
    #function:-1

The last item shown is the value returned after executing the code.

*Note: The console works by creating a module, executing the code, and then exporting all its global variables. The next execution will then inherit those global variables. Anything declared with `var`, however, will be lost.*

To exit, use Ctrl+C.
