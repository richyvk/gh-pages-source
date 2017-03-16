---
layout: post
title: Programming for Everybody (Python) notes
date: 2015-01-14
description: Notes from the University of Michingan Python course
---

I recently did most of [Dr Chuck's Python course](https://www.coursera.org/course/pythonlearn) on Coursera, and documented most of what I'd learnt. Here are my notes, and few comments on the experience.

I'd recommend it for an introduction. It's focused on text processing, but includes all the conceptual elements I expected. Coupled with Swaroop's course: [A bite of Python](http://www.swaroopch.com/notes/python/) and [Learn Python the Hard Way](http://learnpythonthehardway.org/), it represents pretty much the entirity of my Python courses to date.

## Week 1: introduction - why we program

I can’t say I really learnt anything in the first week, but it was definitely fun. Dr Chuck is a charismatic and enthusiastic teacher and his lectures, that are kind of like fireside chats, certainly got me interested in the course.

## Week 2: variables and expressions

Still pretty basic, but I definitely learned some stuff this week.

### Expression evaluation order

When Python evaluates expressions the following hierarchy of operators is used: Parentheses; Powers; Division, multiplication, remainder; Addition, subtraction; Left to right.

An example:

{% highlight python %}
# The expresion to be evaluated
x = 1+2 * 6**2 / 10

# No parentheses, so first would be powers - 6**2 = 36
x = 1+2 * 36 / 10

# Next is Division, multiplication, and remainder
# We have multiplication and division so left to right
# kicks in - 2 * 36 = 72
x = 1 + 72 /10

# Now division - 72/10 = 7 #working in integers of course
x = 1 + 7

# Lastly simple addition, and the final result
x = 8
{% endhighlight %}

### Floats in expressions

When evaluating an expression that contains a float the evaluation is done with integers until the float is evaluated, then after that the rest of the expression is evaluated as if all numbers were floats

### An improvement on the elevator program

My version of Dr Chuck’s Euro > US elevator floor converter. Mine accepts 0 and negative floors

{% highlight python %}
eurofloor = int(raw_input("Enter European floor number: "))

if (eurofloor <= 0):
    print "US floor equivalent is: Basement"
else:
    print "US floor equivalent is:", floor
{% endhighlight %}

## Week 3: conditional code

### Indenting and blocks

Don’t mix tabs and spaces when you indent your code, infact, don’t use tabs at all, indent your code blocks by 4 spaces. To set this is Sublime Text, go to Preferences > Settings - User, and add:

{% highlight json %}
{
  "tab_size": 4,
  "translate_tabs_to_spaces": true
}
{% endhighlight %}

### The if statement

You can do single line if statements like this:

{% highlight python %}
x = 5
if x == 5: print x
{% endhighlight %}

You don’t need to have an else in a conditional, you can just have if and elif(s):

{% highlight python %}
x = 5

if x > 10:
    print "Large"
elif x < 2:
    print "Small"

print "All done"
{% endhighlight %}

I was curious about why Dr Chuck didn’t use parentheses when writing out if conditionals, turns out for conditional statements they do the same thing as for evaluating any simple expression, i.e. to force hierachy of evaluation! So, they are really not necessary for simple conditions like x < 5.

I think I will still use them though, for consistency if nothing else.

### try/except

Try/except is used to deal with errors, by default it will only deal with run time errors, e.g. non-existent variables. An if statement will never raise an exception on it’s own. You have to use 'raise' to get that to happen.

It may be possible to use 'assert', but that has its own issues apparently.

## Week 4: functions

I’m sad to say I didn’t really learn anything new about functions from Dr Chuck. To be fair, he did say functions wouldn’t really feature in the course. I would suggest looking elsewhere for function related tutorials.

Format for a function:

{% highlight python %}
def function_name(argument1, argument2):
    # indent code inside function by 4 spaces
    print argument1, argument 2
{% endhighlight %}

## Week 5: loops and iteration

A loop that never runs is known as a zero trip loop, for example:

{% highlight python %}
x = 0

# loop will never run because x is set to zero, and condition is x > 0
while (x > 0):
    print x
    x -= 1
{% endhighlight %}

Use continue in a loop to return to the start of the loop, for example:

{% highlight python %}
while True:
    data = raw_input()

    if (data == "skip"):
        print "returning to top of loop"
        continue #data will not get printed, focus is returned to data = raw_input()
    print data
{% endhighlight %}

While type loops are known as indefinite loops, they will contune to run until some condition becomes false, the opposite are definite loops, i.e. iteration

{% highlight python %}
# for loop (iteration) example

x = [1,2,3,4,5]

#prints numbers 1 to 5
for i in x:
    print i
{% endhighlight %}

Loop idioms was a phrase I’d not come across before, Dr Chuck gave examples including counting, adding and averaging loops. More on idioms on wikipedia.

## Week 6: Strings

Best thing I learnt this week is the dir function. Use it to discover built in methods for an object, e.g. a variable that points to a string object:

{% highlight python %}
#super useful!
>>> string = "Hello World!"
>>> dir(string)
['capitalize', 'center', 'count', 'decode', 'encode'...
{% endhighlight %}

Access a character from a string using indexing:

{% highlight python %}
string = "Hello World!"
print string[1] #prints e (2nd character, as indexing is form character 0)
{% endhighlight %}

Get length of string:

{% highlight python %}
string = "Hello World!"
print len(string) #prints 12 (number of characters in string)
{% endhighlight %}

Looping through strings:

{% highlight python %}
#Indefinite loop
string = "Hello World!"
index = 0

while index < len(string):
    letter = string[index]
    print letter
    index += 1

#definite loop
for letter in string:
    print letter
{% endhighlight %}

Slicing strings:

{% highlight python %}
string = "Hello World!"
print string[0:5] #prints first 5 characters (upto but not including index position 5)
print string[6:] #prints from 6th character to end of string
print string[:] #prints all characters
{% endhighlight %}

'in' as an operator:

{% highlight python %}
string = "Hello World!"
'H' in string #True
'h' in string #False
{% endhighlight %}

A simple string parsing exercise:

{% highlight python %}
#find the host an in email given from_line
from_line = "From John Smith (john@email.com.au)  Date 1 December 2013 Subject: Hi!"

# index position of first @ symbol in from string
at_position = from.find('@')

# index position of first ) after @ symbol in from string
closing_paren = from.find(')', at) 

# prints characters in from string between index positions for @ and ),
# i.e. the email host
print from[at + 1:close_par]
{% endhighlight %}

## Week 7: You Have Arrived

Didn't make any notes this week.

## Week 8: Lists

Lists are mutable! Use the range function to create a list of integers:

{% highlight python %}
>>> print range(4)
[0,1,2,3]
{% endhighlight %}

Not sure when you would need it really, but if you want to use the index of an item in a list when looping through it you can combine range() and len() to do that:

{% highlight python %}
list = ['a','b','c']

for i in range(len(list)):
    print i, list[i]
although in the above example, this would also work:

list = ['a','b','c']

for i in list:
    print list.index(i), i
{% endhighlight %}

Lists can be concatinated (+) and sliced ([n:n]) just like strings. Interesting that concatination builds a new list from the existing lists, I thought it might have created a new list of nested lists, but no!

An aside, two logiccal operators to remember: in and not in:

{% highlight python %}
>>> list = ['a','b','c']
>>> a in list
True
>>> d in list
False
>>> b not in list
False
{% endhighlight %}

Interesting discussion on alternatives to loop idioms discussed in week 5:

{% highlight python %}
#averaging loop - week 5 version
count = 0
sum = 0

while True:
    inp = raw_input("Enter a number: ")
    if inp == 'done': break #note single line version of if statement
    count +=1
    sum += inp

print "Average: %d" % sum / count

#the same thing can be done by adding inputs to a list then performing
#the calculation on the list using built-in functions(methods)
list = []

while True:
    inp = raw_input("Enter a number: ")
    if inp == 'done': break
    list.append(inp)

print "Average: %d" % sum(list) / len(list)
{% endhighlight %}

The idea of adding values to a list via a loop and then later doing other things with that list, i.e. with those values, is a powerful one!

The split() method splits a string into a list:

{% highlight python %}
>>> string = "The quick    brown fox"
>>> listy = string.split() #default split character is space (any number of spaces count as one)
>>> print listy
['The', 'quick', 'brown', 'fox']
or provide an argument to split on another character
>>> string = "Hello-World"
>>> listy = string.split('-')
>>> print listy
['Hello', 'World']
{% endhighlight %}

Split() method can be really useful for extracting specific elements form large strings, e.g text files. Use the "double split" method, split on white space, then refine by taking important items form the list and spliting those with other chracters.

### Guardian patterns

A technique form preventing errors in your programs, for example, if it appears specific data being reed might be causing problems. Basically debug to figure out what data is causing the issue and then write a statement to deal with that data before the bit of your program that crashes is reached.

Typically this would be an "if x: continue" statement.

## Week 9: Dictionaries

Didn't make any notes this week.

## Week 10: Tuples

Basically immutable lists. They are iterable like lists, but you can't change them once created so you can't sort, append etc. So why use them? Because they are more efficient than lists. Useful for assigning multiple variables in one statement:

{% highlight python %}
(a, b) = (10, 20)

#We don't really need the parentheses on the left hand side, so:
a, b = (10, 20)
{% endhighlight %}

Useful for iterating over keys and values in dictionaries:

{% highlight python %}
myDict = {'a': 1, 'b': 2, 'c': 3}

for (k, v) in myDict.items():
    print 'key is %s and value is %d' % (k,v)
{% endhighlight %}

Tuples are comparable:

{% highlight python %}
>>> (1, 2, 3) < (1, 3, 5) #Comparisons start from left, if first values are equal comparison moves to next values in each tuple
True
>>> ('a', 'b', 'c') > ('a', 'b', 'd')
False
{% endhighlight %}

Because they are comparable they are sortable, so are useful for sorting dictionaries by key:

{% highlight python %}
>>> myDict = {'a': 1, 'b': 2, 'c': 3}
>>> l = myDict.items() #first convert dictionary to list of tuples
>>> print l
[('a', 1), ('c', 3), ('b', 2)]
>>> l.sort() # then use sort() to sort by keys
>>> print l
[('a', 1), ('b', 2), ('c', 3)]
{% endhighlight %}

You can combine all the above and use the ```sorted()``` method to output sorted keys and values:

{% highlight python %}
>>> myDict = {'b': 2, 'a': 1, 'c': 3}
>>> for k,v in sorted(myDict.items()):
...     print 'key is %s and value is %d' % (k,v)
... 
key is a and value is 1
key is b and value is 2
key is c and value is 3
{% endhighlight %}

Dr Chuck talked a little bit about refactoring, suggesting once you understand the long form of writing many of these idioms, you can often refactor them into 'more dense' versions. An example of this being if oyu wanted to get the top 5 most common words in some text data:

{% highlight python %}
# First read the data and record the word frequency
source = open(data.txt)
counts = {} #dictionary to store word counts

for line in source:
    words = line.split()
        for word in words:
            counts[word] = counts.get(word, 0) + 1

#Then do the sorting of the word count dictionary to get the top 5 words
lst = [] 

for k,v in counts.items():
    lst.append( (v,k) ) #add value and key tuples form counts to lst

lst.sort(reverse=True)

for v,k in lst[:5]:
    print k, v

#the sorting can be refactored as:

lst = sorted([(v,k) for k,v in counts.items()], reverse=True)

for v,k in lst[:5]:
    print k, v
{% endhighlight %}
