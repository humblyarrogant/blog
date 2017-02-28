+++
date = "2017-02-28T12:03:53+01:00"
title = "Code Review: Sanity Checks"

+++
For the most part, sanity checks are put into the code to ensure there are no bugs. For this reason, guaranteeing sanity checks are done correctly becomes necessary. If you do not check to see if the data is valid, and it is invalid, then you're going to allow invalid data to proceed. Here, I'm going to discuss how I think we should do sanity checking in PHP.

## Asserting Valid Data

What I've seen a lot is people are asserting for invalid data when they're doing their sanity check. While this makes logical sense, if it's data you know to be invalid, then obliviously you want to stop your application at this point.

However, I feel that what we should be doing, instead, is checking whether or not the data is valid instead of invalid. The number of ways data can become invalid through the lifecycle of a project can be numerous; however, the ways the data can be valid remains the same until the code is changed.

## Type Strict Checking

One of the issues with this approach is that it's checking to see if the value is null; however, in weakly-typed languages, it's possible for the return value to be a range of values, which aren't null, but not the correct value we're wanting. This occurs, especially in PHP, where developers have a habit of returning false in error cases. So, it can be quite common that, at some point, this method could return false but still not be the value we want.

### Here is some example code with this problem:

<div><script src='https://gist.github.com/1f894e6e1bd7c1054c83998a20f3d768.js?file=one.php'></script></div>

### Here is how I think it should be done instead:

<div><script src='https://gist.github.com/1f894e6e1bd7c1054c83998a20f3d768.js?file=two.php'></script></div>

For the second snippet, I check to see if it's not numerical. So, instead of starting with a value that I don't want, I declare the type of data I do want and only fail if I don't get that type. By doing this, I now have a more versatile codebase since a small error of returning false in a method that a developer was expecting null doesn't break the application.

## Object checking

So, another issue I've seen is where people do checks to see if a non-true value has been returned when they want to see if they have a valid object to use. However, this doesn't check if they have a value object, and it could be a case that they have a true value or a completely different object that doesn't uphold the contract they want to use.

### Here is some example code with this problem:

<div><script src='https://gist.github.com/1f894e6e1bd7c1054c83998a20f3d768.js?file=three.php'></script></div>

### Here is how I think it should be done instead:

<div><script src='https://gist.github.com/1f894e6e1bd7c1054c83998a20f3d768.js?file=four.php'></script></div>

So, instead of checking to see if I had an object or a true value, I checked to see if I had the type of object I wanted to use. This means if someone returns a different object type that doesn't have the contract, I then want to use the code fails as we expect it to.

## Other Solutions

These issues could be solved by using strict typing and correctly analysing the code so that your build fails if you inject a string into a method that expects an integer. For many teams and projects, using these tools aren't immediately available or even possible, so if you use PHP 7, have strict typing enabled, and run Etsy's Phan on strict, then you'll discover a lot of these issues automatically.

You will still have issues where the type is correct, but the value isn't correct. So in cases where you're checking a string value, is one of the expected string values, then you would need to check that the value is still the sort you want and that it's not just an empty string.

## Open Source Projects

Also, some may wonder why other projects like Symfony don't do it this way. Well, it's simple: they code review the other way, and they make sure their contracts are all valid and that they never break a contract. Since all their contracts are very strictly documented and very heavily reviewed, they're able to be more confident that the code they're using won't change.

You also need to remember how long an average pull request takes to get merged and how many people review them. A pull request to an open source project can take weeks to be merged and be reviewed by dozens of developers. Whereas, generally, within companies, pull requests last hours or days and are reviewed by one or two developers. In my opinion, this increases the need for such defensive programming measures.

There is also the point that, with projects like Symfony, if a contract isn't being upheld it's a bug in the method returning the incorrect type, and that's where it must be fixed. However, for in-house applications, you don't care so much where the bug is; you care more that you don't have bugs in the first place.

## Conclusion

Hopefully this explains some of the ways we can do sanity checking wrong. It's important to note that these sanity checks aren't just for checking return values, but also set values on class variables and other sorts of places that sanity checks need to be done.
