---
title: Install
layout: default
---

## Download

Binaries and source can be downloaded from [here](http://nekovm.org/download).

You may also compile and install Neko from source.

## Installation

Installation can be accomplished by following the instructions on the [main site](http://nekovm.org/doc#installation). You will also need to install *libgc*, which is available from [here](http://www.hpl.hp.com/personal/Hans_Boehm/gc/), but is usually installable via a package manager. For example, on Mandriva, `sudo urpmi libgc`.

The main issue is having the binaries (*nekoc*, *neko*, *nekotools*) in your path and all the libraries included with Neko (particularly *libneko*) available in either LD\_LIBARARY\_PATH or NEKOPATH. This is where Neko will look for all libraries, including those that are user-created. Note that Neko will work equally well no matter where it is placed, as long as the paths mentioned above are set up correctly.

### Compiling for 64-bit

If you are compiling Neko on a 64-bit machine, you will want to remove the `#` from the following line in the Makefile:

`CFLAGS += -D_64BITS`

### Compiling for OS X

If you are compiling Neko for OS X, you will want to remove the `#` from the following line in the Makefile:

`MACOSX = 1`

### Compiling OS X Universal Binaries

If you want to compile OS X universal binaries, you will want to remove the `#` from the following line in the Makefile:

`OSX_UNIVERSAL = 1`

### Compiling for low memory usage

You can compile Neko to use less memory (and more CPU) by removing the `#` from the following line in the Makefile:

`CFLAGS += -DLOW_MEM`
