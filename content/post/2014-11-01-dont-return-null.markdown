---
layout: post
title: "Don't return null"
date: 2014-11-01T15:12:23+01:00
comments: true
categories: [development, theory]
---
If you're programming in an object orientated language that supports exceptions you should never return null in a method that returns an object.

<!-- more -->

Most object orientated languages support exceptions. Exceptions give us an extremely expressive way to represent error conditions. We throw an exception and the program bails out of where it is and then goes to the error handling section. We can create custom exceptions to express exactly what sort of error occured. This is how error handling in object orientated programming languages is meant to be done

Returning null on error comes procedural programming. In procedural programming it makes a lot of sense. In most procedural programming languages there is no other way to represent an error condition. The problem here is the user of the method has to do the error checking and manually handle the error.

Generally in the method where an error condition has occurred, there has been sort of logic check to see if everything is ok or if it's an error condition. If we're returning null then we have to do this logic again every time we use this method. Where as with an exception there is only the logic check in the method and then all the error handling is handled by try/catch switches.

When a method is meant to return an object developers naturally want to chain method calls on this. It just feels very natural and generally looks a lot cleaner. When we do this and an exception is flung our code just jumps to the exception handling. If we return null we end up with an error for calling a member method on a non object. In PHP a fatal error.

Throwing an exception instead of returning null, allows you to keep your code more consistent. You can make sure that methods always return a value of the same type. Removing the need for repeating the same sanity checks all over your code.

So in overview we have more valid object orientated code, less repeating yourself, more consistent code, more expressive code, and cleaner code. Those all sound like pretty good reasons to stop returning null.
