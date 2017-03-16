---
layout: post
title: University of Toronto funciton design recipe
description: foo
---

I’m doing this course, to transition to Python 3 mainly. But, I’m already discovering why it’s so well regarded, and that I have much to learn!

I really like there function design recipe, it goes like this:

1. Write some examples of what you want your function to do:
    ```python
    >>> some_function(arg)
    some_result
    >>> some_function(arg2)
    some_other_result
    ``` 
2. Write the type contract:
    ```python
    (parameter types) -> return type  # e.g. (number, number) ->int
    ```
3. Write the function header, with meaningful names:
    ```python
   	def meaningful_func_name(meaningful_param_names):
   	```
4. Write the description. Explain what is returned, and mention parameters explicitly.
5. Write the body of the function (the actual code).
6. Test using the examples written in point 1.

Points 1, 2 and 4 become the docstring for the function, which can be called using help(function_name). The final function might look something like this:

{% highlight python %}
def ellipse_string(long_string):
    """(str) -> str
    Returns a string equal to the first 5 characters of long_string followed by ...
    >>> ellipse_string("Hello, World!")
    'Hello...'
    """
    return long_string[:5] + '...'
{% endhighlight %}
