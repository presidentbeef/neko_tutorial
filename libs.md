---
title: Libraries
layout: default
---

## Importing from C Libraries

The standard libraries and the libraries shipped with Neko (e.g., Regexp) are C libraries with an API layer to interact with Neko. The difference between these libraries and modules written in Neko is only in how they are imported.

Importing from a library looks like this:

    $loader.loadprim("\[library\]@\[function\]", num_arguments);

For example, to load the `file_open` function from the standard library, which takes two arguments, the call would be:

    var open = $loader.loadprim("std@file_open", 2);

The imported function can then be used like any other function.

Similarly, if one wished to import the `regexp_new` function from the Regexp library, one would do:

   var new_reg = $loader.loadprim("regexp@regexp_new", 1);
