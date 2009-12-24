---
title: Tools
layout: default
---

## neko

The `neko` command will run a file which contains compiled Neko bytecode. If the file has a `.n`, you can omit it.

`neko <bytecode_file>`

### Interpretive mode

To disable the JIT and only run interpreted code, use

`neko -interp <bytecode_file>`

### Statistics

Some limited statistics are available using

`neko -stats <bytecode_file>`

This will print out how much time is spent in some functions and how many times they are called. It is mostly limited to C function calls.

## nekoc

### Compiling

The primary purpose of `nekoc` is to compile Neko code to Neko bytecode. It will output a file with the file's extension replaced with `.n`.

`nekoc <source_file>`

### Linking

Several bytecode files can be joined together into a single file.

`nekoc -link <output_file_name> <bytecode_file> <bytecode_file> ...`

This is very useful if you are planning on building a stand alone executable using `nekotools`.

### Console

There is a read-execute-print loop available using `nekoc`. To use this, type in the code and then `!` to execute it. The results will be shown.

`nekoc -console`

_Note: local variables (declared with `var`) will not be kept in scope after the `!` is used to execute the code._

### Dumping bytecode

It can also dump the bytecode from a compiled file. It will output a file with `.dump` as the extension.

`nekoc -d <bytecode_file>`

### Stripping bytecode

Debugging information and global names can be stripped from compiled bytecode. This is done in place, it does not create a new file.

`nekoc -z <bytecode_file>`

### Prettifying code

`nekoc` can also create a properly formatted version of a source file. This command will create a new file. For example, if the source file is named "test.neko", the new file will be called "test2.neko".

`nekoc -p <source_file>`

### Documentation

Documentation can be produced from comments in Neko source code. This will produce an HTML file.

`nekoc -doc <source_file>`

### Options

Verbosity can be turned on with `-v`.

The output directory can be set with `-o <directory>`.

## nekotools

### Webserver

You can run a webserver that serves up pages using Neko code.

`nekotools server`

Options:

+  `-h <domain>` - set hostname
+  `-p <port>` - set port
+  `-d <directory>` - set base directory
+  `-log <file>` - set log file
+  `-rewrite` - activate pseudo mod-rewrite for smart urls

URLs will be matched to `.n` files in the server directory. For example, http://localhost:2000/test/ will execute and display the results from `test.n` file, if it exists.

### Standalone executable

It is possible to create standalone executables from Neko bytecode. Note, however, that you will probably still need `libneko.so` or `libneko.dll` unless they are statically linked to `neko`.

This will output an executable file with no extension.

`nekotools boot <bytecode_file>`

## nekoml

This program compiles NekoML files.

`nekoml <source_file>`

