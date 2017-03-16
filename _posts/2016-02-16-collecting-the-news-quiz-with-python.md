---
layout: post
title: Collecting The News Quiz with Python
description: foo
---

I love [The News Quiz](http://www.bbc.co.uk/programmes/b006r9yq)! After [Ed Readon’s Week](https://en.wikipedia.org/wiki/Ed_Reardon%27s_Week) I reckon it’s my favourite English comedy radio show. To listen to it I subscribe to the BBC’s [Friday Night Comedy](http://www.bbc.co.uk/programmes/p02pc9pj/episodes/downloads) podcast via Pocket Casts on my phone. [Pocket Casts](http://www.shiftyjelly.com/pocketcasts) is a great podcatcher app but it makes archiving files for future listening very tricky, not least because it renames all the mp3 files it downloads to some random generated hash looking thing. I really wanted to keep my own archive of the show outside of my phone, so I can burn them to CD and make my partner listen to them in the car for example. So, I decided to see how hard it would be to do this with Python. Turns out it was pretty much trivial.

First up import required modules, I used just standard library plus [Beautiful Soup](http://www.crummy.com/software/BeautifulSoup/) to parse the podcast RSS.

{% highlight python %}
import datetime
import urllib
from bs4 import BeautifulSoup
{% endhighlight %}

Next define a function to actually download the mp3 file if it’s found in the feed. This is super simple using urlretrieve. The function takes two arguments, the url for the file and the filename to save the file as locally.

{% highlight python %}
def dl(url, filename):
    """download mp3 file using urllib.urlretrieve"""
    print "Downloading {0} from {1}".format(filename, url)
    urllib.urlretrieve(url, filename)
    print "Downloading complete"
{% endhighlight %}

Next define the function that actually checks the podcast feed to determine if there’s anything to download. The Friday Night comedy podcast generally includes a short season of The News Quiz followed by a few weeks of other stuff I didn’t want to keep, so after parsing the feed with BeautifulSoup the function checks the title element for the first item in the podcast feed. If it contains ‘the news quiz’ the dl function is called.

{% highlight python %}
def check_rss(url):
    """check rss feed for News Quiz episodes"""
    feed = urllib.urlopen(url).read()
    soup = BeautifulSoup(feed, 'tml.parser')
    item = soup.find('item') #find first item tag in feed
    title = str(item.title.string).lower()
    link = str(item.link.string)
    mp3_title = title.replace('fricomedy: ', '').replace(' ', '_') + '.mp3'
    #download mp3 if title tag string contains 'the news quiz'
    if (title.find('the news quiz')):
        dl(link, mp3_title)
{% endhighlight %}

Lastly, I run this as a scheduled task on my [Pythonanywhere](http://www.pythonanywhere.com/) box. Unfortunately you can only schedule daily or hourly tasks on Pythonanywhere and I only wanted it to run once a week, on a Monday. So, I set up a daily task and used the datetime library to confirm the week day and call the check_rss function on Monday only.

{% highlight python %}
today = datetime.date.today()
weekday = today.weekday()
if (weekday == 0):
    check_rss('http://tinyurl.com/zlggdje')
else:
    print "No download today, it's not Monday"
{% endhighlight %}

That’s it. Super easy and works just fine until the BBC decide to change the url of the podcast feed or the titles of the episodes. I’ll deal with that if it happens, but for now my News Quiz collection grows nicely.

PS. I’m aware I should probably send some specific user agent data when making the request for the feed. Apparently urllib sends something generic. I’ll probably rewrite this script using requests at some point which makes sending headers a lot easier.
