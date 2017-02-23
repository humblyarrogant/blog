---
layout: post
title: "Social Engineering defence"
date: 2014-04-13 19:40:14 -0400
comments: true
categories: [security, theory]
---
So a while back I read a blog post by [ChunkHost](http://www.chunkhost.com/blog/15/huge_security_hole_in_sendgrid) about a "Huge security hole in Sendgrid". And instantly I thought why isn't there a protection against something which is so obviously dodgy. After a few seconds I thought of an easy protection against such an attack, I've now found time to write about it so here it is.

<!-- more -->

#The attack

The attack was simple, someone phoned up Sendgrid's customer support and talked them into changing the email for the ChunkHost account from support@chunkhost.com to support@chunkhost.info. Once they did that they then did a forgotten password request. Once they had access they then add their email as a BCC to all emails going out. At this point they then targeted chunkhost customers with forgotten password requests. The attack on the end targets failed as they used two factor authentication.

#Review

First major "WHAT?" is that Sendgrid allowed the email to be changed over the phone, but hey that's what this attack is about tricking someone into doing something for you. So lets get on two the other things. One of the things I would consider blatantly off, is changing an email from a .com to a .info for your login. I can see this happening in the sending of emails but why would anyone move from the arguably best TLD to one that is one of the least favourable? I can't see that happening that often. Next is that straight after the email is changed there is a forgotten password request. That to me would ring alarm bells. Then there is the fact you can BCC transactions email in the first place.

#Conclusion

It seems to me all of this could be easily stopped by preventing people from doing forgot password requests within 24 hours of changing their email. While this may be really annoying from a UX point of view, in 99% of cases people can wait 24 hours to log in to something. Also when they do a forgot password within 24 hours of changing their email, send an email to the old email account that there is a forgot password request and ask them to contact customer support. That would allow people a change to quickly react if there is an attack on their accounts. 

Also obviously using two factor authentication on your logins will also prevent social engineering attacks like this. Since even if they can do a forgot password request and get the login details they won't get the other authentication factor. This one wins out overall. But if you're unable or unwilling to implement two factor authentication you can at least apply the 24 hour delay on password changes with ease.

*TL;DR Stop people from doing forgot password for 24 hours after changing emails. Or just use two factor authentication.*

