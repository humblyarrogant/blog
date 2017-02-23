---
layout: post
title: "Revel : How to use Drone.io for testing"
date: 2014-04-26 20:39:14 -0400
comments: true
categories: [development, revel, testing]
---
Being a lover of testing, continuous intergration, and cloud services. I wanted to be able to get a build of status of a Revel framework app I'm working on. Since Revel uses it's own command to run and build applications the standard way of doing a build for Golang are out. I wanted to use [Drone.io](http://drone.io) instead of travis so if I wanted to make it private I could without paying a lot. So taking the .travis.yml wasn't an option either. It was shockingly simple to set up. It took 3 lines.

<!-- more -->
# The 3 lines

A quick breakdown of what is going on. First you install the revel framework, then you install the revel command. Then you call the revel command with the test command using import directory that will be used by go when it grabs your code. So in my case it was "**revel test github.com/icambridge/sitrep**". 

{% gist 11329286 gistfile1.txt %}
