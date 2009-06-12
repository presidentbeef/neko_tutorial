---
title: Debugging
layout: default
---

## Error Messages

### "Uncaught exception - Invalid call"

This error message is usually shown when a function is called with the wrong number of arguments.

### "Uncaught exception - $\[function_name\]"

This is usually the result of calling a built-in function with the wrong type of argument.

### "Uncaught exception - load.c(176) : Module not found : \[module_name\]"

Neko was unable to load the given file, either from the command line (`neko <name>`) or from a call to loadmodule.
