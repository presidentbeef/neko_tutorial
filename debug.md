---
title: Debugging
layout: default
---

## Error Messages

### ./neko: error while loading shared libraries: libneko.so: cannot open shared object file: No such file or directory

This message occurs when Neko is unable to find the libneko library, which is required to run. Make sure that *libneko.so* (or *libneko.dll* on Windows) is in your path.

On Windows, you can check your path with `echo %PATH%`. You can (temporarily) set your path with `set PATH=%PATH%;c:\neko` (if that is where you put Neko). You can set this more permanently following the directions [here](http://support.microsoft.com/default.aspx?scid=kb;en-us;310519&sd=tech).

On Linux, you can use `echo $LD_LIBRARY_PATH`. Setting your path (if you are using bash) is done with `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/neko`. Add this to your *~/.bash\_profile* to have it set every time you log in.

### Exception : (file\_contents, \[file\_name\])

    Called from neko/Main.nml line 130
    Called from core/Args.nml line 43
    Called from core/Args.nml line 50
    Called from neko/Main.nml line 44
    Called from neko/Main.nml line 28
    Exception : (file_contents, [file_name])

This usually means the specified file could not be found when trying to compile it.

### Uncaught exception - Invalid call

This error message is usually shown when a function is called with the wrong number of arguments.

### Uncaught exception - $\[function\_name\]

This is usually the result of calling a built-in function with the wrong type of argument.

### Uncaught exception - load.c(176) : Module not found : \[module\_name\]

Neko was unable to load the given file, either from the command line (`neko <name>`) or from a call to loadmodule.

### Stack alignment failure

Find any code that looks like

{% highlight javascript %}
if(true)
    var x = 1;
{% endhighlight %}

and change it to

{% highlight javascript %}
if(true) {
    var x = 1;
}

*Note:* It's the `var` part that does it. So if you can move that outside the `if` block, that will work as well.
{% endhighlight %}
