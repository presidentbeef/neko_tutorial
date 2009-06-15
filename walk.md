---
title: Walkthrough
layout: default
---

## Notes

In this tutorial, commands which should be entered at the command line look `like this`.

## Installation

Follow the instructions [here](install.html).

Make sure you can run Neko from the commandline by trying the commands `neko` and `nekoc`. 

## First Program

Create a new file called *hello.neko*. In that file, put the following:

    $print("Hello, Neko!\n");

Save the file. From the commandline, first make sure you are in the same directory as the file you have created.

Then run `nekoc hello.neko`. This will compile the program, producing a new file named *hello.n*.

Now you can run your first program using `neko hello`.

This simple program uses the built-in `$print` function, which takes any number of arguments and prints them out to the screen. The semicolon ends the expression. However, semicolons are, in general, optional.

Characters enclosed in double quotes (") are strings.

## Creating Functions

The following code wraps the code above in a function:

    function() {
        $print("Hello, Neko!\n");
    }

If you compile and run this new code, you will not see anything. That is because we created the function, but did not do anything with it. Since functions are just values (like strings, numbers, booleans, objects, etc.), we can assign it to a variable. Then we will be able to call or invoke it.

Since Neko is a dynamically typed language, variables do not need to be declared with a specific type.

    var hello = function() {
        $print("Hello, Neko!\n");
    }

    hello();

Note the use of parentheses to actually call the function. In this case, there are no arguments to pass in, so we simply use an empty pair of parentheses.

What if we wanted to be able to pass in some arguments? Not a problem:

    var hello = function(name) {
        $print("Hello, ", name, "!\n");
    }

    hello("Bob");

## Creating objects

Objects in Neko are quite simple. They are essentially just a collection of fields, accessible via the dot notation. Continuing our example, we can have the hello function be a field on an object:

    var hello_object = $new(null);

    hello_object.hello = function(name) {
        $print("Hello, ", name, "!\n");
    }

    hello_object.hello("Bob");


The `$new` function creates a new object. If the argument to `$new` is null, it will create an empty object. One may also pass in an object to `$new`, which will then return a copy of that object.

Since functions are just values, we also could have created the object like this:

    var hello_object = $new(null);

    var hello = function(name) {
        $print("Hello, ", name, "!\n");
    }

    hello_object.hello = hello;

    hello_object.hello("Bob");


