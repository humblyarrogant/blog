---
layout: post
title: "Observer pattern in golang"
date: 2014-03-22 10:37:14 -0400
comments: true
categories: [development, code, golang]
---
For some reason at some point, I thought it would be hard to implement the observer pattern in Go. Then I made an issue for me to blog about it. Well it's not hard. It's as easy as it is in every 
other language.

<!-- more -->

# Observers

First part of the observer pattern is you need the actual observers. The logic that you want executed whenever something happens. Here I've just put a simple log print statement that will print out the name of the hook to the log. 

Created an interface to allow for more flexible typing later on.

{% gist 9708081 interface.go %}

# Observer Notifier

The main part of the logic, simply have an add observer and then have a process function that loops through and calls them all.

{% gist 9708081 observer.go %}

# Full

Here is a copy of it all together. As you can see it's really simple to whack together once you have a half decent understanding of Go.

{% gist 9708081 main.go %}
