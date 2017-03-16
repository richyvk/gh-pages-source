---
layout: post
title: JS Math object - some useful bits
description: foo
---

I hate Maths (or Math as it’s known in some parts). I hate it because I’m rubbish at it, I don’t understand it, it does my head in, and it doesn’t excite me at all.

That said, I recently learned some stuff that the Javascript Math object can do that I can see I will use in the future, so I’m documenting it here.

### Math.min/Math.max
Find the lowest/highest number in a range

{% highlight javascript %}
Math.min(1,20) //1
Math.max(5,90) //90
{% endhighlight %}

### Math.floor/Math.ceil
Round a floating point number down/up to the next integer

{% highlight javascript %}
Math.floor(9.8768); //9
Math.ceil(8987.987); //8988
{% endhighlight %}

### Math.round
Round a floating point number to the nearest integer

{% highlight javascript %}
Math.round(3.67); //4
{% endhighlight %}

### Math.random
Return a random number between 0 and very close to 1, e.g.

{% highlight javascript %}
Math.random() //0.7083173703867942
{% endhighlight %}

This means you can do this to get a random integer within a desired range:

{% highlight javascript %}
function getRandomInt(min, max) {
 return Math.floor(Math.random() * (max - min + 1)) + min;
}console.log(getRandomInt(10,50); //25
{% endhighlight %}

### Rounding
Not Math methods but hey…

{% highlight javascript %}
toFixed(n) - round to n decimal places
35.980134701.toFixed(2); //35.98
toPrecision(n) - round to n precision
35.980134701.toPrecision(6); //35.9801
{% endhighlight %}

### isNaN
Check if a value is a number or not, returns true if not a number

{% highlight javascript %}
//Prompt for an age until a number is given
do {
  userAge = prompt("What's your age?");
} while (isNaN(userAge));
{% endhighlight %}
