---
title: Booleans
layout: default
---

## Boolean Values

`true` and `false` are used for true and false, respectively. However, any value may be converted to a boolean using the `$istrue` function, which returns false for `false`, `null`, and `0`, and true for anything else. The `$not` function does just the opposite. For `if` and `while` expressions, only `true` will be considered true.

## Boolean Operations

`&&` is logical "and" and `||` is logical "or". These operations are short-circuited and do not convert the values to booleans.

For example:

{% highlight javascript %}
$print(false || "Hello"); //prints "Hello"
{% endhighlight %}

