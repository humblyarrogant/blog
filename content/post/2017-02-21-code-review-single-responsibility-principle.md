+++
title = "Code Review: Single Responsibility Principle"
date = "2017-02-21T15:12:23+01:00"
+++
Single Responsibility Principle (SRP) is probably one of the most well-known principles from SOLID. At its core is a desire to prevent classes from becoming overwhelming and bloated. While enabling the ability to change how a single thing works by only changing a single class. So the benefits of SRP are that you have an easier codebase to maintain since classes are less complex and when you wish to change something you only have to change a single class. In this blog, I will go through some ways to try and help avoid breaching SRP while doing code review.
<!--more-->
## The Manager/Service

A manager or service is a class which has been created to deal with everything related to a certain thing. Generally these are created to enable SRP, however, in the majority of cases they generally end up being the main source of non-compliance of SRP.

In discussion with other developers about a newly created

As an example I will create an InterviewManager:

<div><script src='https://gist.github.com/68a3a7ccd3739f566b108be76a4831e2.js?file=InterviewManager.php'></script></div>

In the above class there are quite a few methods, while they all relate to interviews there are many responsibilities being held within this class. The following responsibilities can be found within this class:

* Data Storage
* Validation
* Scheduling

### Data Storage

So within this class, we have three methods are for just storing data. This is when we create, delete, or read data. This responsibility could change and all the other logic within this class would not have to change.

### Validation

We have a method isInterviewValid, again this isn't related to any other method in this class other than they all work on Interview.

### Scheduling

We have three methods that relate to scheduling interviews, those being scheduleInterview, postponeAllInterviewsForPerson, and automaticallyAssignInterview. With automaticallyAssignInterview arguably being another responsibility since I could schedule an appointment without it being assigned to anyone, however, it could also be considered scheduling since it schedules it for the other party.

### Solution


<div><script src='https://gist.github.com/68a3a7ccd3739f566b108be76a4831e2.js?file=InterviewManager.solution.php'></script></div>

In this solution, I've just split the Manager class into three separate classes: InterviewRepository, InterviewScheduler, InterviewValidator. Thus allowing for the proper encapsulation of the responsibilities in each class.

## From Usage

Sometimes we can spot SRP isn't being adhered to by the usage of the code. One of the ways to identify these cases is when a return value from one method is being used as a parameter for another method in the class.

### Example code:


<div><script src='https://gist.github.com/68a3a7ccd3739f566b108be76a4831e2.js?file=InterviewController.php'></script></div>

Like in the previous scenario, we've got an overloaded Manager class, however, this can happen with many types of classes. So the responsibilities of the lines of code are:

* Data storage
* Interview Assignment

The responsibility overload of data storage and interview assignment in the same class is quite clear, however, what I think isn't so clear is that there is also a responsibility of saving the data. Somehow automaticallyAssignInterview has to save the data since we're not seeing any call to a save method. Which means the automaticallyAssignInterview somehow has to save it. Which means that method even if just moved to another class would be helping breach SRP.

### Solution


<div><script src='https://gist.github.com/68a3a7ccd3739f566b108be76a4831e2.js?file=InterviewController.solution.php'></script></div>

In this solution, we create two classes and call the repository to fetch the data and then assign the interview and then save the data. While this does increase the number of lines within the controller this allows for a more clear understanding of what is happening within the method, as before it wasn't explicit that the data was being saved.

## Conclusion

Hopefully, these examples will help you to better understand methods of detecting and correcting SRP infractions during code review.
