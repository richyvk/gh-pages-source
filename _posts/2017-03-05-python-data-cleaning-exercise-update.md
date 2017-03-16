---
layout: post
title: A data cleaning exercise with Python - an update
description: foo
---

Back in October 2015 I wrote this post about cleaning up some data in one of our databases. he problem was essentially two-fold. Remove duplicates and then retain items that were not found in a validation list.

I'm writing this as a first new post on this the newest incantation of my blog as a way of charting how far I've come in 18 or so months.

Here's How I did the original version:

{% highlight python %}
# process the data file
with open('data-file.txt') as dataFile:
    dataList = dataFile.read().splitlines()

# and the same for the validation list
with open('validation-list-file.txt') as validationFile:
    validationList = validationFile.read().splitlines()

# remove duplicates
uniqueDataList = []
for item in dataList:
    if item not in uniqueList:
        uniqueDataList.append(item)

# function for filter() to use on uniqueDataList
def compare(element):
    if element not in validationList:
        return True

# filter data against validation list
onlyInData = filter(compare, uniqueDataList)
{% endhighlight %}

Twelve lines of code (plus comments). I was pretty chuffed with that back then!

Here's how I'd write it now:

{% highlight python %}
# process the data file
with open('data-file.txt') as dataFile:
    data_list = dataFile.read().splitlines()

# and the same for the validation list
with open('validation-list-file.txt') as validationFile:
    validation_list = validationFile.read().splitlines()

# remove duplicates
unique_data_list = list(set(data_list))

# filter data against validation list
only_in_data = [item for item in unique_data_list
                if item not in validation_list]
{% endhighlight %}

So that's a 50% shorter script. Back then I had no idea what a [set](https://docs.python.org/3/tutorial/datastructures.html#sets) was, or heard of [list comprehension](http://treyhunner.com/2015/12/python-list-comprehensions-now-in-color/). Oh, and I'm a bit more [PEP8](http://pep8.org/) compliant these days!

It's funny reading a lot of my old code now. My current code is far from amazing, but it's certainly better than it was. 

The moral of this story - keep going, you will improve!

