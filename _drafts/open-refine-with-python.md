---
layout: post
title: The power of OpenRefine and Python
description: foo
---

I discovered OpenRefine a few mnths ago, after a quick demo at RezBaz 2017 by my friend @weaverbel.

Since then I've tinkered with it, but recently I've had cause to use it at work to clean up some pretty yukky data in our library catalogue. I've needed to do some fairly complex stuff, and so it was a revelation to me to learn that it is very easy to use Python (well Jython acctually) to transform cell contents, and do all sorts of awesome stuff.

OpenRefien ships with Jython 2.5.1 which means you are limited to Python 2.5 functionality. Not exactly cutting edge, but still very very useful offering a raft of options to edit data over and above what you can do with OR's own GREL language.

The principle is the same for harnessing Jython to do both facets and transforms in OpenRefine. From the dropdown on the column you wnat to work with select either Facet > Custom Text Facet, or Edit Cells > Transform. You could also, for example, do Edit column > Add column based on this column if you don't want to disturb your source column.

Then select Python/Jython form the Language dropdown, and away you go.

The one thing to remember is you must always end your code with a return statement. What ever you ultimately return will be what ends up faceting or transforming the cells in the column. I think of it as a giant function without having to define it using ```def foo:```

Other than that it's pretty much regular Python. You can import modules, define variables, and even write helper functions etc along the way to get to your final return statement.

Here are just a few of the handy things I've learned you can so.

## URL encoding/decoding

If you have a long complex url, you might want to have the contents in a more huuman readable form. For that you can use Python's urllib.quote() method.

{% highlight python %}
# Example for transforming values for all cells in a selected column

import urllib
return urllib.unquote(value) # value is a variable that points to the current contents of each cell

# To encode you can do the opposite

import urllib
return urllib.quote(value, "=") # second argument is characters to ignore when encoding, e.g. =
{% endhighlight %}

## URL splitting

Another useful tool for working with long and complex urls, is the urlparse module.
