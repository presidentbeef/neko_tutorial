---
title: Questions
layout: default
---

These are some questions which have come up on the mailing list. If there is a question you need answered, please ask on the mailing list. If there is a question and you have the answer, please use the link at the bottom of the page to contribute to this site.

#### Profiling - Is there a profiler for Neko?

No, not really.

You can get some idea of what is going on using the `-stats` argument to `neko`, but it is quite limited.

There was an attempt to create a profiler for Neko, which can be enabled in the `Makefile`, but it is currently broken.

#### Debugger - Is there a debugger for Neko?

No, not currently.

#### Line numbers - How do I get the original line numbers when exceptions are raised?

You can use [NXML](http://nekovm.org/doc/nxml) to specify line numbers. Note that any NXML file MUST literally begin with `<nxml>` and end with `</nxml>`.

#### NXML - Why is it generating invalid modules?

One person had this issue because you need to specify at least one file/line number in the NXML code.

#### Tail Call Optimization - Why does it fail when using variable-length arguments?

Tail calls performed in functions which are wrapped using `$varargs` will not be optimized, as wrapping the function this way creates a call to C and a callback to the NekoVM.

#### Linking using nekoc -link fails

Apparently, combining modules via `-link` is quite limited at the moment. There does not seem to be much one can do other than fixing the linking code itself.
