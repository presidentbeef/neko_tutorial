---
title: Strings
layout: default
---

## Neko Strings

Strings in Neko are just arrays of bytes, so they may hold any binary data. Like arrays, they are indexed beginning with zero. There is also a standard library for dealing with strings as UTF8 characters [here](http://nekovm.org/doc/view/utf8). Strings may hold up to 2<sup>29</sup> - 1 bytes, and cannot be resized once they are created.

## Literal Syntax

The literal syntax for Neko strings uses double quotes (`"`). Special characters may be escaped using a backslash (`\`). These characters are:

+ `\"` - Double quote
+ `\\` - Backslash
+ `\n` - New line
+ `\r` - Carriage return
+ `\t` - Tab
+ `\xxx` - Decimal binary code between 000 and 255

{% highlight javascript %}
var s = "Hello!\\nTab\\tover\\\\there";

$print(s);
{% endhighlight %}

## Creating Strings

An empty string (populated with `null` values) can be created using `$smake` and a specified size:

{% highlight javascript %}
var s = $smake(10);
{% endhighlight %}

A copy of a string may be created using `$scopy`:

{% highlight javascript %}
var s = $scopy("neko");
{% endhighlight %}

## Accessing Strings

Individual bytes can be accessed using the `$sget` function which takes an index and returns an integer representing the value at that index. `null` is returned if the index is out of bounds.

{% highlight javascript %}
var s = "neko";

$print($sget(s, 1)); //prints "101"
{% endhighlight %}

Substrings may be accessed using the `$ssub` function, which takes a string, a starting index, and a length. If these are out of bounds, an error is raised.

{% highlight javascript %}
var s = "neko";

$print($ssub(s, 1, 2)); //prints "ek"
{% endhighlight %}

## Modifying Strings

`$sset` will set individual bytes in a string to the given integer value between 0 and 255. Returns `null` if the index is out of bounds.

{% highlight javascript %}
var s = "neko";

$sset(s, 2, 110);

$print(s); //prints "neno"
{% endhighlight %}

To copy chunks of one string to another, use the `$sblit` function. This takes a starting position in the destination string, a starting position in the source string, and a length of the substring to copy. Raises an error if anything goes out of bounds.

{% highlight javascript %}
var src = "neko";
var dst = "hello";

$sblit(dst, 2, src, 2, 2);

$print(dst); //prints "hekoo"
{% endhighlight %}

## String Size

The size or length of a string is returned from the `$ssize` function.

{% highlight javascript %}
var s = "neko";

$print($ssize(s)); //prints "4"
{% endhighlight %}

## Finding a Substring

The `$sfind` function can be used to find the first occurance of a string inside another string, starting at the given position.

{% highlight javascript %}
var s = "hello neko hello";

var pos = $sfind(s, 6, "ell");

$print(pos); //prints "12"
{% endhighlight %}

