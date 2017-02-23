---
layout: post
title: "Why hacking on production code during an interview is a good thing"
date: 2014-03-21 18:53:00 +0000
comments: true
categories: [development, random]
---
*Wrote this ages ago and just found it and figured I should post it.*

A while back I saw a blog post ([link](http://hownottohireadeveloper.blogspot.co.uk/2013/11/no-i-will-not-hack-on-your-codebase-for-free.html)) saying that he would never hack on a production code base during the interview. Since he was not getting paid for it. Well I strongly disagree with that, both from an interviewee and an interviewer point of view.

<!-- more -->

# Interviewer

While working at my last job I was in charge of the technical test for developers. Instead of doing what was previously done which was get someone in and then test them. Which simply put wasted a bunch of time since most people were unable to pass the test, so you would waste 30 minutes talking to them and then find out that they can’t do the job in the first place. So instead of having them come in and then test them, what we did was test them before we even arranged an interview. In

The technical test that was in place when I was hired, was in my opinion faulty. It was a selection of how do you do this, how do you do that, spot the errors in this code, what is this, and spot the errors in this query.

My problem with how to do this and how to do that questions in a technical test is that they generally ask how to do really simple things that you only really ever do when you’re starting out after a while you start automating to the point where you never do it. For example how to create a MySQL table. Off the top of my head I could give you a rough query that looks kinda like how the actual query looks. But it won’t work as the syntax will be wrong, I will have put the auto increment in the wrong place, put a comma after the column type field. When in reality I’ll use a GUI tool of some sort to do this, since it’s not something you generally do a lot it’s something you forget. Also when people come up with these questions it’s things they currently know but not always what they knew when they started that position. (Someone else originally made this point, but I can't find who by googling so credit to the anonymous person)

My problem with spot the error questions is they are generally designed to catch people out. If you sit and spent an hour trying to catch people out, unless you’re really stupid you are going to be successful. Especially when you’re looking for syntax errors like a missing bracket, left a quotes open, etc. There is a reason why IDES, text editors highlight code syntax. It’s because it’s really hard to spot these errors. If you’re scanning 25 lines of code and find 8 errors. There is a pretty good chance you’re thinking you’ve found them all. Except you missed the one where it was a comma instead of a full stop. 

So with this all in mind. I created my test or to put it better tests. We had an IRC bot to give out information to the operations team. I had a list of things I wanted automated to make their lives easier. As this wasn’t something that would make the company money. I wasn’t allowed to spend time working on it. So instead of me working on it, I used those tasks as developer tests. We would send one out until someone wrote code good enough for us to use (then interview that person) and then start sending out another one. The test a lot of the time was very easy, write a plugin for the PHP IRC bot Phergie that would do something like check a web site is up, check a value in a database, etc and license it GPL V3. The reasons behind this aren’t just exploitation of the work market, the reason to constantly change the test was to stop people being able to cheat on it and send it someone else's successful submission. (This happened after I left and they kept sending out the same test. One of the guys marking the test spotted it was the code he sent in.) It was also to see if they could write code we would use, if you can’t write code that we would use why do we want to interview you? You’re clearly not up to the job. This test saved us interviewing 3-4 people a week to interviewing 1-2 people a month. Interviewees were pretty much always offered a job after an interview except in one case where it was a personality thing.

# Interviewee

I’ve never actually been asked to hack on production code in an interview but I would love it if I was. Yes I would be giving them my work for free. But at the end of the day I don’t do my job for the money, I do it because it’s what I want to do. My last job I took because they were importing 50 million rows into MySQL twice daily, with 100 queries per second on that data. It was a challenge I’ve never had, it was fun. My current job I took because they allow me to unit testing and do continuous integration. 

But hacking on their codebase gives me something very important. A chance to see what I’ll be working with, a chance to see how good my co-workers will be, a chance to look at their deployment, and a chance for my code to do the talking. Because let’s be serious an interview is not just their chance to check you it, it’s your chance to check them out. If all you get is a couple of people talking to you asking some questions and then giving you a chance to ask questions at the end. It doesn't seem like it's as good an opportunity. Also I never seem to ask any good questions anyways. 

# Open Source Instead?

In the post it was suggested that’ll he’ll hack on something open source and give something back. While in theory this totally awesome, in practice it seems like something that isn’t practical. Such was what open source project? What you going to do in that open source project? While there is always stuff needing done in open source projects, some are really hard to contribute to (WordPress for example) others don’t really have a list of stuff that they need done feature wise.

One place I interviewed at ([Parallax](http://parall.ax)) had another way, they asked me in for a hack day and asked if I had anything I wanted to code as a side project and then had me code that in their framework of choice. Then it was out for beers afterwards, pretty good interview. Turned out to be a kickass company, who I would readily suggest to anyone looking for digital agency or a job. 

# Conclusion

While I could be worrying about am I getting paid for my work, I choose to worry about things I find more important. I’ve also noticed I also have a habit of working a lot of unpaid overtime. I obsess over my work. So worrying if I’m working for free isn’t something I worry about. I’ve found people who worry about getting paid for their work are the ones who don’t have a passion for what they do, leave 5 seconds after their contracted time. Which is fair enough. I would just rather my work was an enjoyable part of my life. Instead of working for the weekend.
