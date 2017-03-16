---
layout: post
title: Creating an RSS feed for Australian Commonwealth Bill changes with Python 
description: How I created an RSS feed to alert on changes to Bills before the Cth parliament using Python.
---
The story of my first real attempt at making something useful with Python.

## The need

I needed a way of keeping track of the progress of Bills before the Australian Federal Parliament (House of Reps and Senate).

In theory this should be possible using the [parlinfo](http://parlinfo.aph.gov.au/parlInfo/search/search.w3p) search engine, but I had a hard time figuring out how. There are also a few RSS feeds [hosted](http://www.aph.gov.au/help/rss_feeds) by the APH site but none of them fit my need either. The closest was the [Bills Digest feed](http://parlinfo.aph.gov.au/parlInfo/feeds/rss.w3p;adv=yes;orderBy=date-eFirst;page=0;query=Date%3AthisYear%20Dataset%3Abillsdgs;resCount=100) but that is only for newly introduced Bills, it doesn’t track their progress through Parliament.

## The solution

Then I remembered that the [APH homepage](http://www.aph.gov.au/) has a ‘Latest updates to Bills’ section which does update as Bills progress through parliament, and links of to a nice homepage for each Bill containing all the information one might need when researching a Bill (EMs, second reading speeches etc).

So the solution was clear, scrape that section of the APH homepage and turn it into an RSS feed. Easy!

## Part 1: scraping

For this I used [Beautiful Soup](http://www.crummy.com/software/BeautifulSoup/) (version 4.3.2 to be precise). I initially though of using [Scrapy](http://scrapy.org/) but that seemed overly complex for this task, so Beautiful Soup won.

Beautiful Soup is an html parsing module for Python. For the purposes of this project it can be understood as an easy way of extracting information from an html page for future use. Once you create a Beautiful Soup object containing the html, you can then very easily search it and extract only the bits you want to use.

It took only a few lines of code to extract all the relevant information I needed from the APH page, storing them as variables that later end up as the content for the RSS feed:

<!-- img -->
![extracting information from the APH homepage using Beautiful Soup](/img/aph_rss_img_1.png)

Probably the only things to mention about the scraping code are that on line 15 the first item in the list of ```<tr>``` elements is removed ([using](https://docs.python.org/2/tutorial/datastructures.html) ```.pop()```) because it contains only headings for the table and is therefore not required.

Note also that the resulting list of ```<tr>``` elements is reversed on line 16. This is required so that the resulting bill_strings are created and processed oldest to newest.

Oh, and I also had to specify the text encoding when building my bill_string, for some reason the result was not good without doing that.

The bill_strings look something like this: ```20 Aug 2015: Gene Technology Amendment Bill 2015, http://www.aph.gov.au/Parliamentary_Business/Bills_Legislation/Bills_Search_Results/Result?bId=r5489``` and contain all the information needed for each Bill entry in the final RSS feed.

## Part 2: preserving the Bills update data

This is where I ran into a challenge. Of course the bill_strings created with Beautiful Soup could be put into a list which could then be turned directly into a feed. However, this would mean the feed would only ever contain the six Bills listed on the APH site — not much of an improvement over going and looking at the site itself, and not really what I wanted.

Instead, I wanted to capture the changes to Bills over a longer time period, which of course meant some sort of data preservation. Options I considered where a database (overkill at this point) and pickling. [Pickling](https://docs.python.org/2/library/pickle.html) would be fine (I think — didn’t actually prove that) except that it’s not easy to human read pickled data directly, which I wanted to do. So for this task I chose to preserve my data in a simple text file.

Thankfully reading and writing plain text is super easy in Python. Here’s the new code including reading and writing bill_strings to the text file:

<!-- img -->
![Storing the bill_strings in a text file for later conversion to the RSS feed](/img/aph_rss_img_2.png)

The preservation happens in three parts:

1. On lines 5 and 7 the existing text file containing previously preserved bill_strings is opened, and converted to a list of existing bill_strings.
2. On line 35 newly created bill_strings are added to the list of existing bill_strings if they are not already present.
3. Finally, on line 40 the existing text file is reopened and its contents replaced with the updated list of bill_strings.

Things to note:

* Opening the file in a+ mode on line 5 means the file will be created if it doesn’t already exist, i.e. the first time the script is run.
* The print statement on line 36 is just an alert that a new bill has been added, printing to standard output.
* Comparing each bill_string to the list of existing bill_strings before adding it to the existing_bills list (line 35) prevents all the bill_strings being added each time the script runs.

## Part 3: creating the RSS feed

The last piece of the puzzle was to create an RSS feed from the list of bill_strings. For this I used the [PyRSS2Gen](http://www.dalkescientific.com/Python/PyRSS2Gen.html) module. There weren’t many options that I could find, and it seemed very easy to use so I went with it.
Again, the code was pretty straight forward, here it is:

<!-- img -->
![The final RSS creating script in full](/img/aph_rss_img_3.png)

Notes on this step:

* Firstly the RSS creation only triggers if new Bills have been added, thus avoiding unnecessary recreation of the feed. To do this a variable new_bills_added is set to False on line 7. It is then set to True on line 42 when a new bill_string is added to the existing_bills list. Finally, the code block creating the RSS feed only runs if new_bills_added is True (line 50).
* The guts of the feed, the [RSS items](http://www.rssboard.org/rss-specification#hrelementsOfLtitemgt), are created by splitting bill_strings back into their original element of date, Bill title and url, and then converting these to RSS items with PyRSS2Gen.
* The lastBuildDate for the feed is set using Python’s very handy [datetime](https://docs.python.org/2/library/datetime.html) module

## Final thoughts

There is one limitation to the feed at this point, which is that if a Bill appears in the latest updates table multiple times on the same date (possible if debated multiple times in a day for example) then it will only appear in the feed the first time it appears. This is a real limitation of the script, and one that was causing me too many headaches to get around. In the end I decided that being alerted to the change in a Bill’s status once per day would be acceptable to most people.

I have been [messing around](https://github.com/richyvk/APH-RSS) with the script since I wrote this version, attempting to make it more modular and I added an FTP component so the feed gets FTPed to a server once the script has run. This is probably a silly way to go about this project and is overkill. I should probably focus on making it more [Pythonic](http://blog.startifact.com/posts/older/what-is-pythonic.html). I will continue to tweak things and refine it if I feel like messing with it some more.

Refactoring is likely also required/desirable. It’s pretty fast now, but it could be faster I imagine. I put lots of comments in and perhaps made things overly verbose in order for relative newbs like me to understand what’s happening.

The feed is up and running though if you want to use it: [http://pittstreetpress.com/Resources/APH-rss/feed.xml](http://pittstreetpress.com/Resources/APH-rss/feed.xml)

Or check out the [current state](https://github.com/richyvk/APH-RSS) of the script on github.