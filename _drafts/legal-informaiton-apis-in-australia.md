---
layout: post
title: Legal information APIs in Australia
description: An overview of the legal information API landscape in 2017.
---

The rise of the API (Application Programming Interface) in recent years is undeniable. The web has matured from its 1.0 status of static read only content, through the buzzing 2.0 read/write years, and has rapidly become something else - a platform for rich fully functioning applications.

Web applications require, and are largely concerned with, data. APIs allow those applications to transfer data to each other efficiently, thus allowing for the creation of even richer, more complex and integrated applications for web users to enjoy.

Take a look at almost any of the big social web applications that exist now (e.g. Facebook, Twitter, Instagram, Spotify) and you’ll find they offer a publicly accessible API that developers can use to build their own applications on top of.

This article will examine the extent to which Australian legal information providers (legal publishers, governments, legal information aggregators) have made APIs available to the public or their customers, and discuss some of the ways that legal information APIs could develop in the future.

## What is an API?

Before we continue though, let’s define what we mean by an API and how they work.

For the purposes of this article, I’m using the term API to mean a web API that allows data to be received from a remote application in response to a request for that data via the Internet. It is possible, and quite common, for APIs to allow for changing data at the remote location (e.g. posting a tweet to a particular Twitter account) but that functionality is outside the scope of this article. Although it is entirely likely that this kind of functionality might be desirable, for now we are concerned with investigating how possible it is to get legal information via an API only.

A typical modern web API will often be based on the REST principles. I won’t go into what this means, not least because I will embarrass myself. What I will say is that the kind of API this article is concerned with would likely follow those principles.

In practice we can define a legal API as:

* Is publically available or available to custopmers
* Uses http to deliver data
* Delivers data an API like this allows you (as the developer of an application) to make standard HTTP requests to the remote provider (publisher etc) and receive a response back in a format that can be incorporated into your application with the minimum of effort — typically this is now JSON (JavaScript Object Notation) but previously has been (and sometimes still is) XML.

## What is the current situation with legal APIs in Australia?

Free sources:

* Federal register of Legislation — no API offered that could be located
* State legislation sites
* AustLii
http://www.austlii.edu.au/techlib/webdev/cgiapi.html
* Jade
A 2011 blog post I located purports to detail a public API for Jade https://jadeful.me/2011/11/21/barnets-jade-api-explained-convert-your-blogs-to-jade-in-seconds/
But it isn’t really an API, rather it’s a useful description of the url patterns Jade employs for accessing specific cases via a media neutral citation. This is useful, but it’s not what this article is concerned with for two reasons. Firstly, the responses are in HTML format at best (or are simply links to the Jade platform). No other data formats, like JSON, are offered. Secondly, the API is for accessing specific cases only, with no option to get data based on search metadata. More on this aspect of what a real legal information API might look like later.

Subscription sources:
* CCH
* LexisNexis
http://www.lexisnexis.com.au/aus/products/lexisnexisAU/tools/default.asp
* Thomson Reuters
* Others — Timebase etc

## Why don’t Australian legal information providers offer APIs and why should they?

This is where we as librarians need to step up. I my conversations with various providers the number one reason given as to why they have not considered offering APIs to their content previously is because there has been no demand for them.

## What might we want from a legal information API?

Full text or metadata only?

Searching

Linking to specific documents

## What does a good API look like?

* CanLii: http://developer.canlii.org/page
* NY Senate legislation: http://legislation.nysenate.gov/

## What is likely to change in the near future?
