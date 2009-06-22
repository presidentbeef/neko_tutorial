---
title: Hashtables
layout: default
---

## Neko Hashtables

Hashtables are data structures for storing key-value pairs. They are capable of holding more than one value per key, but those values will be available in a last-in first-out manner.

## Creating Hashtables

Hashtables are created using the `$hnew` built-in. This function takes an integer which specifies how many 'slots' the hashtable will initially have. However, all resizing of the hashtable will be handled automatically.

{% highlight javascript %}
var h = $hnew(0)
{% endhighlight %}

## Populating Hashtables

There are two ways of adding key-value pairs to hashtables. Using `$hadd` will add the new key-value pair, but will only hide, not replace, any existing values with the given key. Keys may be any Neko value.

{% highlight javascript %}
var h = $hnew(0);

$hadd(h, 1, "a");

$hadd(h, 1, "b");

$print($hget(h, 1, null));  //prints "b"

$hremove(h, 1, null);

$print($hget(h, 1, null)); //prints "a"
{% endhighlight %}

Alternatively, `$hset` will overwrite the *latest* value set to a given key. If multiple values are set to the same key using `$hadd`, `$hset` will only replace the last value.

The third argument to `$hset` is a function for comparing keys. Passing in `null` will cause the function use the default comparison function.

{% highlight javascript %}
var h = $hnew(0);

$hadd(h, 1, "a");

$hadd(h, 1, "b");

$hset(h, 1, "c", null);

$print($hget(h, 1, null));  //prints "c"

$hremove(h, 1, null);

$print($hget(h, 1, null)); //prints "a"
{% endhighlight %}

## Accessing Hashtables

Values can be retrieved from a hashtable according to their key using the `$hget` function. The last argument in this function is a comparison function; passing in `null` will cause it to use the default comparison function. Note that `$hget` does not remove the key-value pair from the hashtable.

If the key is not associated with any value, `null` will be returned.

{% highlight javascript %}
var h = $hnew(0);

$hadd(h, 1, "a");

$print($hget(h, 1, null));  //prints "a"
{% endhighlight %}

To check if a key is in the hashtable, use the `$hmem` function. This takes a comparison function like `$hget` and `$hset`.

{% highlight javascript %}
var h = $hnew(0);

$hadd(h, 1, "a");

$print($hmem, "a", null));  //prints "true"
{% endhighlight %}

## Interating over Hashtables

The `$hiter` function will iterate over all key-value pairs in the hashtable, passing each pair into the given function. Note that if there are multiple values for a given key, each key-value pair will be iterated over.

{% highlight javascript %}
var h = $hnew(0);

$hadd(h, 1, "a");

$hadd(h, 1, "b");

$hadd(h, 2, "c");

var f = function(key, value) {
	$print(key, " - ", value, "\n");
}

$hiter(h, f);
{% endhighlight %}

## Removing Values

The `$hremove` function will remove a single key-value pair from the hashtable. If there are multiple values for the same key, it only removes the latest one. See the examples above.

## Other Functions

There are two functions for checking the size of a hashtable. `$hcount` will return how many key-value pairs are present in the hashtable. Note that if there are multiple values for a given key, each value will be counted separately.

{% highlight javascript %}
var h = $hnew(0);

$hadd(h, 1, "a");

$hadd(h, 1, "b");

$hset(h, 1, "c", null);

$print($hcount(h)); //prints "2"
{% endhighlight %}

`$hsize` will return the current number of slots in the hashtable, whether they are used or not.

{% highlight javascript %}
var h = $hnew(10);

$print($hsize(h)); //prints "10"
{% endhighlight %}

It is possible, but probably unnecessary, to manually resize hashtables using the `$hresize` function.

{% highlight javascript %}
var h = $hnew(0);

$hresize(h, 10);

$print($hsize(h)); //prints "10"
{% endhighlight %}

The integer hash value of any Neko value can be found using the `$hkey` function. This is different from the `$hash` function, which only hashes strings. It will, in general, not return the same values as `$hash`.

{% highlight javascript %}
$print($hkey("hello"));
{% endhighlight %}
