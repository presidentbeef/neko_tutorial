---
title: Commandline Args
layout: default
---

### Accessing Commandline Arguments

Arguments passed into a Neko application via the commandline are stored as strings in an array on the `$loader` object.

For example, running this

{% highlight javascript %}
$print($loader.args)
{% endhighlight %}

like this

    neko cmdargs.n hello world!

results in

    [hello,world!]

