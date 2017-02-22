---
layout: post
title: "Go dep in Docker"
date: 2017-02-04T15:12:23+01:00
comments: true
categories: [docker, golang, godep]
---
Go's dependency handling has been an area which has been needing unification, over the years. Multiple package managers have been created. The Go community has been working on creating a dependency manager recently, which they plan on getting added to the official toolchain. I've decided to jump on the bandwagon and start using this tool. Here's how I've been using it in docker.

<!--more-->

The first issue I encountered was the command `dep` not being found. It turned out my original docker build file had `GOBIN` pointed to somewhere that was not in the `PATH` env for some reason. Looking at the original `Dockerfile` for golang it `GOBIN` doesn't appear to be set at all. So I've set it to `/go/bin` which has already been added to the path.

The next issue was, I was storing and building my code outside of the `GOPATH`. So I moved where I was storing my code to inside the `GOPATH`. With that done it was just a case of running the `dep` commands.

An example `Dockerfile` can be found below.

{% gist 163763cd1017d8a5319c0c48ec697969 Dockerfile %}
