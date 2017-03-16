---
layout: post
title: A data cleaning exercise with Python
description: foo
---

I was recently met with the challenge ofcleaning some data in one of our databases. There is a field in it that has a validation list (controlled vocabulary) associated with it, but in which the data doesn’t all match with that validation list.

There were around 23,000 entries in the data, and 850 entries in the validation list. There were also, obviously, multiple occurrences of each entry in the data.

My task was two-fold. Firstly to remove duplicates from the data so it contained only unique entries, and secondly to compare those entries to the validation list. The final result being a list of all the entries in the data that were not found in the validation list.

My initial thoughts were that this might be a bit tricky to do, but it turns out I achieved a result very quickly using Python, and just a few lines of code. Here’s how:

## Processing the raw data

I had the data as two text files, one entry per line, so it was easy to process into Python lists for cleaning:

{% highlight python %}
#process the data file
with open('data-file.txt') as dataFile:
    dataList = dataFile.read().splitlines()

#and the same for the validation list
with open('validation-list-file.txt') as validationFile:
    validationList = validationFile.read().splitlines()
{% endhighlight %}

## Removing duplicate data

Next step was to remove the duplicates from the data, simply a matter of adding each item in the list to a new list if it was already in there — I really love that Python can do things like this.

{% highlight python %}
uniqueDataList = []
for item in dataList:
    if item not in uniqueList:
        uniqueDataList.append(item)
{% endhighlight %}

## Comparing the data to the validation list

The slightly more complex bit, that uses Python’s [filter()](https://docs.python.org/2/library/functions.html#filter) function. ```filter()``` took me a while to get my head around, but when I did it was some what of a revelation!

{% highlight python %}
#function for filter() to use on uniqueDataList
def compare(element):
    if element not in validationList:
        return True

#filter data against validation list
onlyInData = filter(compare, uniqueDataList)
{% endhighlight %}

So, what’s happening here is that filter takes a list (or other iterable), and passes each item in it to a function. It creates a new list containing all the items in the iterable for which the result of passing them to the function returns True. I this case, the compare function returns True for every item in uniqueDataList that is not found in validationList.

The resulting onlyInData list can then be dealt with as required, i.e. writing to a file.

So, there we have it. 12 lines of code to do all that!

I do find Python fantastic for doing this sort of data processing, so quick and easy, and so close to English it’s easy to remember the right syntax to use.

All librarians should know a bit of this I reckon!