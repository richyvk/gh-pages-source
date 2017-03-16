---
layout: page
title: Posts
permalink: /archive/
feature-img: "img/clouds1.png"
---
<ul>
    {% for post in site.posts %}
    	<li>
	    	{{ post.date | date: "%-d %B %Y" }}: 
	    	<a href="{{ post.url }}">{{ post.title }}</a>
    	</li>
    {% endfor %}
</ul>