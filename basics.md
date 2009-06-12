---
title: Basics
layout: default
---

## Program Structure

Neko programs are fairly loose in their structure. Variable declarations, function definitions, and instructions may be essentially placed anywhere. Code outside any functions is at the top-level and will be executed as it is encountered. Some simple programs are shown below.

## Built-in Functions

Neko comes with many built-in functions, all of which begin with a dollar sign (`$`). More information about built-ins can be found [here](builtins.html). These functions are always available and may be used anywhere.

## Control Constructs

Neko has several flow control constructs: `if`, `while`, `do-while`, `switch`, and `goto` are all available.

## Variables

Variables may have local, global, or function scope. Variables which use the `var` keyword at their first declaration are local to the current scope and are only available after their declaration. Without the `var` keyword, variables are global.

    var x = 1;  //local
    y = 2;  //global
    f = function() {
        z = 3; //global
        x = 4; //function scope (of previously declared 'x')
    }

    f();
    $print(x, " ", y, " ", z, "\n");  //prints "1 2 3"

## Functions

Functions in Neko are closures which copy their surrounding scope. Local variables declared before the function will be copied into the local scope, while global variables (even those declared after the closure) are accessible via reference. Each instance of a function carries its own environment with local copies of non-global variables.

    var y = 1;
    var f = function(x, z) {
        y = 3;
	$print(w, "\n"); //prints "4"
    }

    w = 4;
    f(1, 2);
    $print(y, "\n"); //prints "1"

Neko does not support default arguments.

You can use a variable number of arguments by wrapping a function with `$varargs`:

    f = $varargs(function(args) {
        $print(args);
    })

    f(1, 2, 3); //prints "[1,2,3]"

*Note: Since `$varargs` is a call to a C function, it will inhibit tail-call optimization.*

## Objects

Objects in Neko are quite simple. They are essentially just a set of fields (instance variables) which may be set and retrieved.

    var obj = $new(null);

    obj.a = 1;
    obj.b = function() { "b" }
    
    obj.b();

Neko objects, by default, do not have any parent classes. You can set the parent class of an object via the `$objsetproto` method. Neko only supports single inheritance. You can also make a copy or clone of an object by passing in an object to the `$new` method.

Note that, when using any of the built-in functions for manipulating objects, arguments which are field names must be hashed using the `$hash` method.

## Manipulating Values

Besides numbers and booleans, everything else in Neko is modified and accessed through built-in functions. Arrays, strings, hashtables, and objects all have a set of functions (listed [here](http://nekovm.org/doc/view/builtins)) for manipulating their values.
