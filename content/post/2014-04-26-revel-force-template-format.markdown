---
layout: post
title: "Revel : Force template format"
date: 2014-04-26 15:39:14 -0400
comments: true
categories: [development, revel, code, golang]
---
So in Revel you can have your template in several different formats: html, json, xml, or txt. This is super awesome. As it allows you to send the same data and display different formats - Obivously. It also determines what template to use based on the http request headers that have been sent. So if your request sends that it accepts application/xml it'll use xml and if you request says application/json it uses json. 

<!-- more -->
All awesome. But what if I want to debug something that should only ever be json. Or even more interesting what if I sent that I accept html and json but with json second in the list. AngularJS seems to do this by default, took me a while to figure out what was going on. So I need a way of forcing revel to just use one file format no matter what the http headers are. Thankfully it's super simple, one line in your controller action to set the Request member's Format member to the desired format and it'll use that.
        
{% gist 11321687 snippet.go %}

So in full example.

{% gist 11321687 test.go %}

