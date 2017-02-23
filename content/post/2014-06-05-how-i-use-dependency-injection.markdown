---
title: "How I use Dependency Injection"
date: 2014-06-05 20:39:14 -0400
comments: true
categories: [development, theory]
---
I've been thinking about dependency injection a lot recently and the best way to do it in a clean manner. I recently changed how I was injecting some dependencies, at code review I was asked why. So I figured I would write a blog post fully stating my current views on how to implement Dependency Injection.

<!-- more -->
There are three main ways of injecting a single dependency, as well as what I would consider two ways of injecting multiple dependencies these are also known as patterns. Each with their own use cases.

# Single Dependency

* Constructor
* Setter
* Method

# Multiple Dependencies

* Service Container
* Factory

# Constructor

The constructor method of injecting dependencies is when you pass the dependency in via the constructor when you're creating the object. This is to be used when the dependency is a required dependency that isn't going to change during the lifecycle of the object.

So use case, an email sender dependency. It's very unlikely that you're going to want to change how you send emails.

<div><script src='https://gist.github.com/fa0cd7160709ac6b6218.js?file=Constructor.php'></script></div>

# Setter

The setter method is when you use a setter to set the dependency after the object has been initiated. You would use this if the dependency isn't a required dependency or if it changes during the life cycle of the object.

Use case for this a dependency on a database connection object in a model. You may want to change databases on a multi tennent application depending on what tennet you're using.

Another use case for the setter method is if you want to use interfaces to show that the object has that dependency. For example the ContainerAware interface in the Symfony2. This allows you to give a class multiple dependencies.

<div><script src='https://gist.github.com/fa0cd7160709ac6b6218.js?file=Setter.php'></script></div>


# Method

The method injection is when you injected it into the method you want to use it in. You would use this when you only need that dependency for that method.

Use case for this would be a date object in a calendar object. Where you would want to use the same object for multiple dates.

<div><script src='https://gist.github.com/fa0cd7160709ac6b6218.js?file=method.php'></script></div>

# Service Container

Service container is when you store you dependencies in an object and then pass that around. This allows you to make all your dependencies easily available wihtout having to worry about injecting them individually.

<div><script src='https://gist.github.com/fa0cd7160709ac6b6218.js?file=container.php'></script></div>

# Factory

Factory pattern is an oldie but a goodie. Here you just create the object you require and return it.

This is good when you need to build up a dependency. For example using an entity with the service container. So you have to clone the entity once it's originally been injected and then you have to clone it each time you want to use it. Using the factory pattern you can hardcode the dependency within that class and then inject the factory.

Here is a sample of the code without a factory.

<div><script src='https://gist.github.com/fa0cd7160709ac6b6218.js?file=factory-wihtout.php'></script></div>

With the factory.

<div><script src='https://gist.github.com/fa0cd7160709ac6b6218.js?file=factory-with.php'></script></div>

# Conclusion

So this is my current opinion on how to implement dependency injection and the different use cases. This will most likely evolve over time as I learn new things.
