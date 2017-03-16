---
layout: post
title: Readifying AustLii
date: 2015-02-14
description: An experiment to improve the typography and readability of the AustLii website
---

I love [AustLii](http://www.austlii.edu.au/). Everyone I know that works in a law library loves AustLii (well, if not the actual site itself, then at least the idea of it). For some time now though, I've found myself increasingly frustrated with it. Specifially, since I've actually had to start reading court decisions in some detail using it, I've concluded that AustLii's current format does not provide for enjoyable, or efficient reading. In short, it sucks for reading!

So, what to do? I mean, if a site's primary funciton is to provide an interface for reading text documents (I'd argue that is AustLii's primary function), then it should at the very least not make that task so tough going for users. But, better than that, I think it should be optimised for that function as much as possible.

So, that was the task I set myself. Optimise AustLii for reading court decisions. I figured it wouldn't be that hard to make it more readable, and therefore usable, with a some pretty basic css changes. Turns out it wasn't.

But before we get into the how, let's ponder the why. Why is AustLii so unreadable? AustLii is, I think it's fair to say, one of the least designed websites around. There is often no css, other than a sprinkling of inline styles, which means it is mostly at the mercy of browsers to provide its visual aesthetic.

## Way back when

I think a lot of the problem comes from the fact that the AustLii site was built a long time ago in web terms. The Wayback Machine's version of the AustLii homepage from 10 years ago is essentially the same as the current one. Things were quite different back then, as we shall see.

The state of the web back in 2004 looked something like this:

* 91.35% of people used Internet Explorer (version 6 was the cutting edge), 3.66% Firefox, only 1.5% Safari and Chrome didn't exist. source
* 91% of monitors were 1024 x 768 or lower. source
* HTML was at version 4 and CCS was at version 2.
* Oh, and of course there were no iPhones or iPads!

So, let's say I'm one of the 47% of people who had a 1024x768 monitor in 2004. Most people suggest working with a maximum of 960px viewport width for that resolution. How does a typical decision look on the AustLii site?

<!-- Add img -->
![AustLii content at 960px](/img/austlii-1024.png)

Of most interest for this exercise is the line length, and it comes in at 140ish characters. With a 800x600 monitor that falls to about 110 characters. That's still not exactly textbook, but it's getting close.

As mentioned earlier AustLii relys on the browser to determine other aspects of the readability, such as font family, size and weight; line height; and whitespace. If we assume the browsers back in 2004 had similar defaults for these attributes as they do today, then unfortunately AustLii was somewhat lacking even then. I'm pretty sure it wouldn't have been alone though.

## Fast forward

Fast forward ten years and AustLii really starts to have problems.

In 2012 NNg moved its [recommendation for viewport optimisation](http://www.nngroup.com/articles/computer-screens-getting-bigger/) to 1440px, and the W3Schools [statistics](http://www.w3schools.com/browsers/browsers_display.asp) on screen resolutions in 2014 are esentially the polar opposite of 2004, with 93% of monitors having a higher resolution than 1024x768.

At 1440px window width, the typical AustLii line length blows out to about 210 characters making reading a tough ask, particularly with those default font and line height settings.

W3Schools [statistics](http://www.w3schools.com/browsers/browsers_stats.asp) suggest browser usage is going the same way too. IE is at 10% and falling, Firefox is the 2nd choice at around 25%, but it's Chrome that currently dominates with around 55%.

## The factors

First, let's look at some accepted standards for readbility on the web starting with line length.

[r9y](http://r9y.org/) seemed a good starting point. It [recommends](http://r9y.org/line-length/) a range of 50-75 characters. The Elements of Typographic Style Applied to the Web [suggests](http://webtypography.net/2.1.2) 45-75 and an optimum of 66, so pretty similar. The one descenting view I could find was [Viget](http://viget.com/inspire/the-line-length-misconception) which arrives at 100 charcters as a new standard.

Then there are the font properties. As mentioned AustLii lets the browser style fonts a lot of the time, which typically means we'll get black 16px Times New Roman with standard line height on a white background.

I'm sure there are plenty of typographic theories on these attributes, but I don't have knowledge of them and I didn't feel like spending a lot of time learning about them for this exercise.

So instead, I chose to look at a few existing sites and see how they approached font styling. The sites were chosen because I like them and/or they seemed to me to be mostly about reading, and in my view they do readability pretty well. Here are the results for a 1440px wide viewport:

Site       | Line length | Container width | Font family                                                                                         | Font size | Line height
---------- | ----------- | --------------- | --------------------------------------------------------------------------------------------------- | --------- | -----------
Medium     | 75 chars    | 700px           | Freight Text Pro, Georgia, Cambria, Times New Roman, Times, Serif                                   | 22px      | 33px
New Yorker | 80 chars    | 690px           | Adobe Caslon Pro, Times, Georgia, Serif                                                             | 20px      | 28px
Pocket     | 72 chars    | 640px           | Chaparral Pro, Serif                                                                                | 21px      | 31.5px
Readbility | 75 chars    | 788px           | Sentinel SSm A, Sentinel SSm B, Palatino Linotype, Book Antiqua, Palatino, Serif                    | 20.8px    | 36.4px

## The specs

For this project I decided to use CSS only. I didn't want to complicate things by having to add anything to the existing HTML, either by hardcoding (impossible for me to do anyway) or with Javascript. That way it would a simple case of linking to (or as will be shown later injecting) a stylesheet to get things looking better.

Taking into account the research above, the basic specification I arrived at was therefore:

* Line width - 75 characters at 1440px window width - two of the four sites I looked at used 75 chars and it's within the generally accepted range.
* Serif font, Georgia if available - notice all the sites specify fancy fonts first, probably supplied as web fonts. I didn't want to do that so I went with a serif font. Georgia is a favourite of mine, and it's pretty ubiquitous.
* 21px font-size
* 31.5px line height

I'm giving myself the option to add other styles like font and backgroung colour, but that's the initial ideal.

## The implementation

Optimising for Chrome at a viewport width of 1440px and using the specs above, implementing was actually pretty straight forward. The only real issue was Austlii's odd mark-up.

![AustLii's lack of divs](/img/austlii-source-1.png)

As we can see they don't really do divs which makes styling all that more difficult.

![AustLii's weird use of ordered lists](/img/austlii-source-2.png)

They also have a habit of using ordered lists for presenting the text of decisions which I'm pretty sure they do to provide paragraph numbering. Let's not go into the semantic issues of this, and just take away the point that it's quite hard to reliably target content on AustLii for styling purposes.

That's why I made the decision to put all my styling on the body tag. I would have rather targeted everything below the navigation section at least, but that just wasn't going to happen.

So, starting with font Chrome's default for paragraphs (and ordered lists) is 16px. We're going to use ems to give a relative size, to do this we can use the target / context = size formula.

```21 (target) / 16 (context) = 1.3125```, so our font size will be 1.3125em

We can use the same formula for line height too. Our desired line height is 31.5px, and the context (font size) is 21px

```31.5 / 21 = 1.5```, so our line height will be 1.5

Font family is straight forward giving final font css looking like this:

{% highlight css%}
body {
	font-family: Georgia, serif;
	font-size: 1.3125em;
	line-height: 1.5;
}
{% endhighlight %}

Lastly, we need to sort out the line length which we can achieve by limiting the width of the body element of course.

It's a little more complicated than the font properties, but the target / context = size formula can help us again here too.

First, we need to know the average number of characters that will fit on a line of a [typical AustLii judgment](http://www.austlii.edu.au/au/cases/cth/HCA/2014/52.html) currently. To do this I set my Chrome window to 1440px wide and used dev tools (alt + cmd + i on Mac) to set the font properties of a paragraph to our new size and family. I chose a paragraph that was actually a list item in an ordered list as these are most common, and factors in the space lost to numbering.

Counting the number of characters on each line in that paragraph and dividing that by the number of lines gave an average line length of 134 characters - that's our context in characters. From that we can calculate our body width size:

75 (target chars) / 134 (context) = 0.55970149253731. If we make the body 55.970149253731% of the viewport we should get 75 characters average line length.

AustLii sets a margin of 20px on the body element inline, and to avoid messing with that we can pad the body the rest of the way to get to our desired width. The calculations go like this:

* Existing left and right margins total 40px - that's 0.02777777777778% of 1440px
* 100% (viewport width) - 0.02777777777778% (for existing margins) - 55.970149253731% (for our body width) = 44.00207296849122%
* 44.00207296849122% is therefore the amount of padding we need to apply to the body to get our optimal line length at 1440px

Just remember that because we're using % for our padding the lengths will vary depending on viewport size, but that's what we want for a more [responsive](http://en.wikipedia.org/wiki/Responsive_web_design) design.

We could divide that 44.00207296849122% anyway we liked to apply left and right padding of course, but for simplicity I split it equally. That gives final css for the body element looking like this:

{% highlight css%}
body {
	font-family: Georgia, serif;
	font-size: 1.3125em;
	line-height: 1.5;
	padding: 0 22.00103648424561%;
}
{% endhighlight %}

## The result

I would love if it AustLii considered doing something simple like this to improve the site's readibility. That would be amazing! but I'm realistic about the chances. That's why I looked around for alternative options and discovered that it's actually pretty easy to inject css into a page using a browser extension. The one I use is [CSS Inject](https://chrome.google.com/webstore/detail/css-inject/fmiohbdblcemacakpnoinjmcelddpjbg?hl=en) for Chrome, but I'm sure there are multiple other for Chrome, Firefox, and maybe even IE? I've also uploaded my [final css](http://pittstreetpress.com/Resources/readifying-austlii.css) so anyone can use it in conjunction with CSS Inject to transform any AustLii decision, or use it as the basis for their own css customising for AustLii.

The final product looks like this:

![the final product](/img/austlii-readified.png)

The final css is essentially what is discussed above, but I added a couple of rules to fix a line height issue with list items, and to make references look a bit nicer. Here it is:

{% highlight css%}
body {
	font-family: Georgia, serif;
	font-size: 1.3125em;
	line-height: 1.5;
	padding: 0 22.00103648424561%;
}

li {
	padding-top: 3px;
}

a[name^="fn"] {
	font-size: .75em;
	font-weight: normal;
	vertical-align: super;
}
{% endhighlight %}

I think this styling is a vast improvement on the default, and I do find decisions a lot easier to read using it. The desired line length has been acheived, and the font properties are vastly better. If anything, I am considering dropping the font size a little, as it does seem slightly larger than necessary. I will use it for a while and see how it goes. If anyone has any ideas for improvements I'd love to hear them too.
