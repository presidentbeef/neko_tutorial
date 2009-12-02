---
title: FFI
layout: default
---

## C Extensions

It is fairly straightforward to wrap C libraries so they may be accessed from Neko. However, there are quite a few details, so this page will only cover getting started. The full documentation is available [here](http://nekovm.org/doc/ffi). 

Any C code that will be used from Neko needs to include the `neko.h` header and link to the Neko library (`libneko.so`, `libneko.dylib`, or `neko.lib` depending on your platform.)

## Getting Started


Here is a tiny example:

{% highlight c %}
#include <neko.h>

//Returns true if int1 > int2
value test_function(value int1, value int2) {
        if(val_is_int(int1) && (val_is_int(int2))) {
                if(val_int(int1) > val_int(int2)) {
                        return alloc_bool(1);
                }
                else {
                        return alloc_bool(0);
                }
        }
        else {
                failure("Expected a couple of integers.");
        }
}

DEFINE_PRIM(test_function, 2);
{% endhighlight %}

This C code declares a function that takes two integers and compares them. Of course, this is a silly thing to write a C function to do, but it demonstrates several important items.

First, any function used by Neko should have a return type of `value`. This means it returns a Neko value. Secondly, any parameters will also have type `value`.

There are several macros provided for testing the base Neko types, such as integers. These all begin with `val_is_`.

In this example, we retrieve a C integer from a Neko integer using `val_int`. There are similar operations for the other types.

The example then returns a Neko boolean, created using `alloc_bool`. If the arguments are not the correct type, a Neko exception is raised using `failure`. This is the equivalent of Neko's `$throw`.

Lastly, we have to "export" the function using `DEFINE_PRIM`, which takes the function and the number of arguments. This makes the function available to Neko.

## Compiling

If you are using `gcc` under Linux, you could comile a C module for Neko called `test.c` using: `gcc -shared -fpic -lneko -o test.ndll test.c`

Note that shared Neko libraries should have the `.ndll` extension.

## Using from Neko

To use the function defined above from Neko, we could use something like the following:


{% highlight javascript %}
test = $loader.loadprim("test@test_function", 2);

$print(test(1,2), "\n");
{% endhighlight %}
