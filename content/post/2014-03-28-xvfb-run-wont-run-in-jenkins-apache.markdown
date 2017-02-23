---
title: "xvfb-run and wkhtmltopdf won't run in Jenkins/Apache"
date: 2014-03-28 22:26:14 -0400
comments: true
categories: [development, Jenkins, testing, debugging]
---
I recently came across a rather unsual error with our testing suite while running on Jenkins. The test would pass on our development environment, not exactly odd in itself. Sadly they aren't exact copies, patch level out and what not. However the test would pass on the Jenkins server if ran via command line. So it wasn't that a minor release had a bug fix that was causing the issue. Since after all my googling on the subject turned up nothing I thought I would write up how I found out what it was and what the cause and solution was.

<!-- more -->

**TL;DR: It was caused by SE Linux, disabled it and everything started working fine. It also fixed an issue where wkhtmltopdf would return an error 1299 wouldn't work when called via Apache.**

So the code that we were testing was a functional test controller, it would generate a pdf and force the download. All the test had to do was check and see if a file was downloaded. This constantly failed on the Jenkins server. The tools we use to generate pdfs is [wkhtmltopdf](https://code.google.com/p/wkhtmltopdf/) and [xvfb](http://www.x.org/archive/X11R7.7/doc/man/man1/Xvfb.1.xhtml) to allow for it to run without a GUI system. So I started trying to debug the command. 

Example command 

> xvfb-run --server-args="-screen 0, 1280x1024x24" /var/lib/jenkins/jobs/xx/workspace/app/../bin/wkhtmltopdf-amd64 --use-xserver "https://localhost/xxx" /tmp/will-this-work.pdf

xvfb-run has an error log file parameter. When I added it, the error file was empty When I ran xvfb-run by itself via Jenkins it gave me the help message, when I called wkhtmltopdf by itself via Jenkins it gave me. So I then added a exec call to the Phing build file to see if just the command would work and if it was a PHP issue. This returned an error code of 1. Which isn't really helpful since the error code just means had problems starting up. I then tried the xvfb plugin for Jenkins, that was pointless as that plugin is for a completely different use. I then installed the terminal plugin, tried the command there and it did the same. However I also ran `id` command to see if it was indeed running as the Jenkins user I tried in CLI. As it turned out I got an extra line (which sadly I didn't keep a copy of) after googling that every result was about SE Linux. I then made the jump to disabling SE Linux. Once I did that via the test started to pass via Jenkins.

Hopefully I've put enough information in this post that if other people Google with this issue they'll find this.
