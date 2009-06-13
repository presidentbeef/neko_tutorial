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
