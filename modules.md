---
title: Modules
layout: default
---

## Neko Modules

Each compiled Neko file is considered its own separate module, with its own scope. Values within the module may be exported by adding it as a field to the global `$exports` object. `$exports` will then be available to outside modules.

When importing a module, the local path is searched along with any paths listed in the `NEKOPATH` environment variable. The paths in `NEKOPATH` should be separated by colons (`:`).

## Exporting Values

Exporting is quite simple, just add any value that should be made accessible into the `$exports` object, using any name:

{% highlight javascript %}
var s = "hello!";

var f = function(x) { x };

i = 100101;

$exports.hello = s;
$exports.identity = f;
$exports.number = i;
{% endhighlight %}

## Importing Values

Values are "imported" by loading in the `$exports` object from another file and assigning it to a variable. Note that the module which is being loaded will actually be executed as it is loaded. This means the `$exports` object may be generated dynamically.

To load in a module, there is a global object called `$loader` with a `loadmodule` method for loading modules. Keep in mind, however, that modules written in Neko are handled differently than those written in C. For loading C modules, see [here](libs.html).

`loadmodule` takes two arguments: the name of the module minus the ".n" extension and a loader object. In most cases, the `$loader` object itself would be used for the second argument.

If the code above were compiled into a file named "test.n", the following code could be used to load it:

{% highlight javascript %}
var test = $loader.loadmodule("test", $loader);

$print(test.hello); //prints "hello!"

$print(test.number); //prints "100101"

$print(test.identity("test!")); //prints "test!"
{% endhighlight %}

The imported object essentially becomes a shared object between modules, so it is possible to modify an `$exports` object at runtime and have the changes reflected in another module. The first block of code below is saved in a module named "test" and loaded by the second block of code. The second block of code calls a function in the first, which adds a new exported value. This exported value is then available in the second block of code.

{% highlight javascript %}
//test.neko

var add_export = function(x) { $exports.more = x };

$exports.add_export = add_export;
{% endhighlight %}

{% highlight javascript %}
var test = $loader.loadmodule("test", $loader);

test.add_export("hello!");

$print(test.more); //prints "hello!"
{% endhighlight %}

The object returned from `loadmodule` also includes the field `__module` which is an abstract value containing information regarding the loaded module. This field can be used in conjunction with the module standard library, documented [here](http://nekovm.org/doc/view/module).

{% highlight javascript %}
var test = $loader.loadmodule("test", load);

var f = $loader.loadprim("std@module_name", 1);
$print(f(test.__module));  //prints "test"
{% endhighlight %}
