---
title: Functions
layout: default
---

## Creating Functions

Function definitions look like this:

{% highlight javascript %}
function(arg) {
    //do stuff
}
{% endhighlight %}

## Arguments

Neko does not support default arguments, but variable argument functions can be created using `$varargs`:

{% highlight javascript %}
var f = $varargs(function(args) {
    $print($asize(args), " arguments given.\n")
});

f(1, 2, 3);
f("a", "b");
f();
{% endhighlight %}

However, it is important to note that functions created using `$varargs` cannot be tail-call optimized.

## Return Values

By default, a function will return the value of the last expression evaluated when the function is called. Alternatively, the `return` keyword can be used the return a value at any arbitrary point in the function.

## Inspecting Functions

It is possible to check the number of arguments a function takes using the `$nargs` function. It will return 0 if the function takes a variable number of arguments.

{% highlight javascript %}
var f = function(arg1, arg2) {
    //do stuff
}

$print($numargs(f));
{% endhighlight %}

## Currying and Closures

While Neko functions are naturally closures (by copying their environment), it is also possible to create curried functions. These functions have some of their arguments applied, but are waiting on the rest.

This can be done using the `$closure` function, which also allows the function's `this` variable to be set (the second argument):

{% highlight javascript %}
var f = function(arg1, arg2) {
    arg1 + arg2
}

var c = $closure(f, null, 1);  //sets first argument to 1, environment is empty
$print(c(2)); //prints "3"
{% endhighlight %}

If there is no need to set the `this` environment, the `$apply` function can be used in a similar manner:

{% highlight javascript %}
var f = function(arg1, arg2) {
    arg1 + arg2
}

var c = $apply(f, 1);  //sets first argument to 1
$print(c(2)); //prints "3"
{% endhighlight %}

