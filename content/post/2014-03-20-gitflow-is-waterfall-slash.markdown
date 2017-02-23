---
layout: post
title: "The git-flow branch model is waterfall?"
date: 2014-03-20 15:23:04 -0400
comments: true
categories: [development, theory]
---
For those not in the know, git-flow is technically a tool for git which allows for the easy use of a specific branch model. Which is most commonly referred to as git-flow.  This blog post isn't about that tool which is super useful. But is about the branch model. Which is also super useful in my opinion if you're implementing the waterfall development process.

**Disclaimer**: *This isn't meant to be a criticism of either the branching model or the waterfall process. It's more me pointing out that it doesn't really fit in with what I consider to be an agile development process if used fully as described. Not to say that implementing some of it can't fit in with an agile development process. Basically I'm trying not to be offensive to anyone. (Also it should be noted that listening to me may result in you looking stupid. You have been warned.)*

<!-- more -->

## Git flow summary

So a quick run through of the branch model if you haven't read [the blog post about it](http://nvie.com/posts/a-successful-git-branching-model/). You basically branch each feature off into it's own **feature branch** and develop that separately from other features. When a feature is finished you then merge it into the **develop** branch. Once you feel you have enough features in **develop** you then merge it in to a **release branch**. At which point you only test and apply bug fixes to that branch and once you're ready to deploy it you then merge it to **master**. Which is to be an exact copy of production. You then tag it once it goes into **master**. Once it's in **master**, and you need to fix some urgent bug in production you would create a **hotfix branch**. Any non urgent bug would be fixed in a **bug branch** that is branched off from **develop**.

So over all you have:

* **feature branch** - Features get developed in these. In isolation so that you can release only fully finished features. Branch name example feature/comments
* **develop** - The main development branch, where all completed features are merged into and feature and bug branches are branched off from. 
* **release branch** - A branch that is suggested to go to production at which point you test and then bug fix before going live. Branch name example release/0.1
* **master** - A carbon copy of production, that tags are created from.
* **hotfix branch** - An urgent bug fix branch, that is branched off from **master**.  Branch name example hotfix/dataleakage
* **bug branch** - A non urgent bug fix, that is branched off from **develop**. Branch name example bug/invalid-email

## Things I like about this branch model

That you develop features off in their own branch. This makes it super simple to keep unready features away from production. Bugs are developed in their own branch allows you to change stuff that may break other things and have the safety you're not breaking everyone else's working environment.

The fact that branches are named so you know the purpose of the branch, if it's a bug, a feature, or the development mainline.

## What I don't like about this branch model 

The **release branch**. Its whole purpose is to implement the testing & bug fixing phase of waterfall. For anyone who has worked on a largish project using waterfall, will know this phase sucks. It just feels like a constant battle. You spend ages testing everywhere by hand, then fix everything you find, then spend more time testing everything by hand. By the end of it,  it feels like you've tested a section 100 times. You get that feeling deep down that you never want to see that section again. This in my opinion is the main problem, if you're like me and get bored silly testing something by hand 100 times you'll want to make it go as quickly as possible. This results in poor testing, which results in a product with more bugs. Since you're holding up all your features on testing in one go, you end up with more spending what seems like more time testing, get bored quicker, and get sloppier. I just can't see an upside to this method of testing by hand.

Also another downside of the release branch and its waterfall feel is that you're not getting feedback quick enough. Say for example you have a financial statement and you only have a single column showing the amount of the transaction. Yet it doesn't tell you if it's crediting the account or debiting the account to the extent the product owner would like. Then say you've then added onto the statement UI to make it load in via AJAX. You then have to change the UI and the AJAX endpoint to return the new data. If you were told when the UI was developed you wouldn't have to go back and change the AJAX endpoint.

Tagging on **master** every time you merge to it. It just seems like you're not very trusting of the whole version control system. I agree that if you're deploying to production you should creating a release a tag should be created, but if every time you commit to **master** seems a bit much. I just feel it's a bit much. Also I think that you should keep your development mainline so stable that it can be deployed at any point without any issue.

## How I feel this branch model should be used

**Feature branches** are used to develop features independently of one another. When the feature is finished the feature is then tested and one agreed to the level of stability that it can be deployed. At which point it is then merged into **develop**. This allows it to be tested and accepted quickly and allow for changes to be made as soon as possible and not result in cascading changes due to requirement changes. It also keeps your development mainline stable enough that you can deploy at any point.

## Conclusion

While I don't think my suggested branch model is anywhere near perfect. It doesn't have that waterfall feel to it. I feel code should be tested as soon as it's written and finished and in small chunks. Yes there should be automated tests, however these don't replace an actual user testing it nor do they replace the product owner looking at it and agreeing that's what they want. The git flow branch model is clearly a successful one since so many people implement it, I just feel it's not for me. 
