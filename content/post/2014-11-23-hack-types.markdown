---
title: "Hack: Types"
date: 2014-11-23T15:12:23+01:00
comments: true
categories: [development, hack, hacklang]
---
Facebook's Hack bring lots of features that a lot of other programming languages get to take advantage of. One of major advantages of Hack over PHP is a typing system. So here's a quick run over of the typing system as I understand it.

<!-- more -->

## Annotate

Annotating is when you define which type is going to be used. You can type the following:

* function arguments
* function return
* class variable
* constants

For function arguments you just put the type before the variable name for the argument.

<div><script src='https://gist.github.com/26159043a232e7206b40.js?file=function.hh'></script></div>

For the return type you just put `: type` in between the function definition and the function body.

<div><script src='https://gist.github.com/26159043a232e7206b40.js?file=return.hh'></script></div>

For constants you just put the type in between the `const` keyword and the constant name.

<div><script src='https://gist.github.com/26159043a232e7206b40.js?file=dd.hh'></script></div>

For class variables you just put the type in between the scope keyword and the variable name.

<div><script src='https://gist.github.com/26159043a232e7206b40.js?file=class.hh'></script></div>

## List of basic types

Primitive are one most basic types that are used in most programming languages.

* `string`
* `int` - Integer
* `float` - Floating point
* `bool` - Boolean (True or False)
* `array`

Primitive Unions are types that can be used to describe other Primitive types that go together.
* `num` - integer or float
* `arraykey` - string or integer

Arrays while being a primitive type can be expanded to show what type of data they hold. You can also define the array key type. Instead of typing arrays like this you may want to look at using collections.

* `array<string>` - An array of strings
* `array<string,int>`  - An array of integers indexed by a string

Classes and interfaces, if a class or interface exists in the code that's being executed then it's a type that you can use for type annotations.

Other basic types

* `mixed` - Will take anything
* `void` - Nothing it means there is no type, this is generally used
* `resource` - A resource such as filepointer, curl resources, etc.
* `(function(typeOne, typeTwo, ...): returnType)` - closure
* `tuple(typeOne, typeTwo)` - tuples

A full list can be found in [hack annotations docs](http://docs.hhvm.com/manual/en/hack.annotations.usingtypes.php).

## Generics

Sometimes you want your code to work with any type. In those cases we can use type generics. Generics can be defined on a class or on a method. To define a generic you wrap the name of the generic with less than and greater than in either the class definition or the method definition.  

When naming it you should remember can't use the name of a type that already exists. It's a general rule of thumb that you start your generic type with `T` and for real simple use cases `T` alone is fine. With collections it's advised to use `Tk` for the key and `Tv` for the value.

<div><script src='https://gist.github.com/26159043a232e7206b40.js?file=generics.hh'></script></div>

## Overriding return type signature

When you extend a class you are able to override the return type for methods you override. However the new type must be compatible with the original type. So in other word the type must be a child type of the original type.

So say you originally typed it `Foo` you couldn't then change the type to `bool`. As that's not a compatible type of `Foo`. However if you created a child class of `Foo` called `Fooable` you would be able to use that as a type. So your code still actually follows the orignal return signature it's just more detailed.
