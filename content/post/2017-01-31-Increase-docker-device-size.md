---
layout: post
title: "Increase docker device size on Ubuntu"
date: 2017-01-31T15:12:23+01:00
comments: true
categories: [devops, Kubernetes, docker]
---
So I've got an application that I'm running via  and Docker. That requires a certain amount of disk space and would run out of space very quickly with the default 10G limit that Docker comes with.

<!--more-->

I figured the easiest way to move forward with this would be too look into if I was able to increase the size of device. It turns out you can. You can pass an option when you're starting docker. The flag is `--storage-opt dm.basesize=15G`. So to run it it would be the below command.

`/usr/bin/docker daemon --storage-opt dm.basesize=15G`

However I wanted to be able to do this while still using the Ubuntu daemon management. To do this I had to edit `/etc/default/docker` and add the line `DOCKER_OPTS="--storage-opt dm.basesize=15G"` and then restart my docker daemon.

Once I did this I noticed new containers weren't being started with the new device size. It turned out that to get docker to use the new device base size I had to delete all my containers and images and pull the images again.
