---
layout: post
title: "RabbitMQ One consumer blocking others"
date: 2017-02-01T15:12:23+01:00
comments: true
categories: [rabbitmq]
---
I've been working on a distributed application that requires multiple workers to process items from a queue. I decided to use RabbitMQ as the queue. However I noticed that there was a 10 minute pause or whenever the consumer started up. After looking into it further I noticed that it appeared that only one consumer could run at any given time.

<!--more-->

After doing a lot of searching and looking at various documents and trying to see if it was the library I was using. I discovered that I had to set the number of items prefetched. Once I did this my consumers were able to start almost instantly consuming.

How I set the prefetch configuration using the Qos command. In Go and in PHP (since I had a PHP version to see if it was just the library in Go I was using.)

{% gist bd7334304dabc1fac3c6a1441a96a561 main.go %}

{% gist bd7334304dabc1fac3c6a1441a96a561 main.php %}
