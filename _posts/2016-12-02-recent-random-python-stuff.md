---
layout: post
title: Random Python stuff I’ve learned recently
description: foo
---

Through trying to shift over to Python 3, and practicing generally, I’ve learned/remembered a few cool Python things in the last few weeks. Here they are:

## String slicing

This can be really useful and powerful:

{% highlight python %}
>>> a_string = "Hello, World"
>>> a_string[:5]  # From start to position 4
Hello
>>> a_string[7:]  # From position 7 to end
World
>>> a_string[7:-1]  # From position 7 to position -2
Worl
>>> a_string[:]  # From start to end
Hello, World
>>> a_string[::-1]  # From start to end reversed
dlroW ,olleH
>>> a_string[::2]  # From start to end with stride of 2
Hlo ol
>>> a_string[::-2]  # From start to end with stride of 2 reversed
drW,le
{% endhighlight %}

Edit: You can slice lists too ( and possibly other things I’m sure). This means you can do cool things like this:

{% highlight python %}
>>> a_list = [1,2,3,4,5,6]
>>> chunked_list = [a_list[i:i+2] for i in range(0, len(a_list), 2)
[[1, 2], [3, 4], [5, 6]]
{% endhighlight %}

## Print statement arguments

You can do this to control the separator characters when using print():

{% highlight python %}
>>> print(*range(1,11) sep='')
12345678910
{% endhighlight %}


## *args

Use *args to pass an unspecified number of arguments to a function, like:

{% highlight python %}
>>> def sum_numbers(*nums):
        return sum(nums)
>>> sum_numbers(12334,2123423524,3245245245245)
3247368681103
{% endhighlight %}

## Starred expressions

This has kind of blown my mind. Instead of this:

{% highlight python %}
for i in range(1,11):
    print(i)
{% endhighlight %}

You can do this:

{% highlight python %}
>>> print(*range(1,11), sep="\n")
1 2 3 4 5 6 7 8 9 10
{% endhighlight %}

## Joining lists

To create strings from list items you can do this:

{% highlight python %}
>>> ", ".join(["Hello", "World"])
Hello, World
{% endhighlight %}

## String formatting

Instead of this:

{% highlight python %}
"Hello" + ", " + "World"
{% endhighlight %}

you can (should) do this:

{% highlight python %}
"Hello, {}".format("World")
{% endhighlight %}

String formatting is very very powerful — you can do fancy stuff like:

{% highlight python %}
>>> print("{:f} apples up on top".format(10))
10.000000 apples up on top
>>> print ("You need {:.2%} less opinions than you think you do"
           .format(46/150))
You need 30.67% less opinions than you think you do
{% endhighlight %}

## List comprehension

You can do this to generate lists of output from a loop (I need to read up on this some more yet):

{% highlight python %}
>>> print([num for num in range(1,11)])
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
{% endhighlight %}

And that’s it for now. More to follow I hope.
