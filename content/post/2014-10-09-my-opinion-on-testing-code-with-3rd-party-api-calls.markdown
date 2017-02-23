---
layout: post
title: "My Opinion on testing code with 3rd party API calls"
date: 2014-10-09T15:12:23+01:00
comments: true
categories: [development, theory]
---
I've recently had a discussion about how I would go about testing code that makes calls to a remote third party API. It seems my way of thinking isn't the same as most others. So I figured I would write out my thoughts and explanation behind why I would go for this route.

<!-- more -->
# Others peoples approach

So first I want to explain other peoples thought patterns seem to be. It goes like:

* Write a wrapper around the API requesting code
* Write unit tests and mock the wrapper
* Write functional tests that include hitting the API

The idea behind this is to make sure your code still works with the API such as it hasn't changed with the functional test. While allowing yourself to just test your code on the unit level. Overall it gets the job done, I just think it's slightly flawed.

# My approach

So here is my plan of action:

* Write a wrapper around the API requesting code
* Write unit tests and mock the wrapper
* Write integration tests that mocks the API
* Write smoke test the API

The idea here is again we allow unit testing by wrapping and mocking. Then with the integration tests we ensure all the code within our application, even 3rd party code all integrate together and that everything goes well when the API returns what we expect. Then we smoke test the API to ensure it hasn't changed and all works the way we expect it to.

# Reason behind my approach

Mocking and wrapping the API requesting code seems like a no brainer that everyone agrees with. We want to own the code we're testing on a unit level. While decoupling ourselves to a certain extent from the third party API.

Mocking the API is where most people think I'm being a bit crazy. I think the fact there is extremely good tools out there to do this such as robohyrda say I'm not that crazy.

The reason I would go down this route is you're decoupling your test suite from the third party API. When you couple your test suite a third party I've found you end up with the following issues.

* Failed builds due to timeout issues
* Failed builds due to API being unreachable completely
* Other people running their tests at the same time and it creates conflicting states on the API
* You spend a bunch of money paying for API calls for your tests
* Your test suite time starts to increase more rapidly

So for these reasons I would want to keep away from hitting third party APIs in my test suite. But yes you still want to test the API works the way you expect, which is why you run a smoke test which isn't an isn't build failure. But something you run on a regular basis to say that you're code will still work or if you need to change out the API requesting code.

# Open to ideas

If you've got another way of thinking I would really interested in hearing it.
