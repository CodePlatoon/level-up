# Typed Languages

## Course Goals

* Explain the difference between a strongly typed language and a weakly typed language
* Explain the difference between dynamic and static languages
* Describe the benefit of using strong vs weak, dynamic vs static languages
* Explain how TypeScript relates to JavaScript

## Summary

Coding languages can be categorized in many ways, some of which explain how “types” are handled within the language. Applying type checking and type safety to programs helps to catch potential errors that could occur if unexpected inputs, outputs, or data transitions occur.

Types refer to the data types, for example String, Integer, or Array. 

## Strongly typed vs weakly typed

Strongly typed vs weakly typed speaks to whether or not you can convert data between types implicitly. To over-simplify, with a strongly typed language you cannot convert data between types, in a weakly typed language, you can.

What does it mean to convert data between types? Another way to say this is with a strongly typed language there are restrictions on conversions between types (ie: String to Array). For example, in python, a strongly typed language, you cannot convert an integer to a string. If we try to say `“TV” + 234` in python, we will get a type error when the program runs.

A weakly typed language does not enforce data type on conversion. For example, in a program for math calculations, you wouldn’t need a strict mechanism to enforce that a method called `total()` needs to take integers as its input.

With a weakly typed language, you can make the language work in ways that may not make sense in other applications. For example, you can add a non-integer to an integer. Obviously in real life applications, an integer would only be added to another numeric value, but we can do something like `“TV” + 234` in some languages and yield a valid result `“TV234”`.

But there is a caveat. Sometimes a strongly typed language can appear to be weakly typed, but some “syntactic sugar” is being applied. Syntactic sugar is syntax within a programming language that is designed to make things easier to read or to express. 

Let’s take Java for example.

```java
String s = "TV" + 234;
```

Would also yield a result as `"TV234"` , but Java is a strongly typed language. So what gives? What’s actually happening here is that a type conversion is being made behind the scenes:

```java
String s = "TV" + new Integer(234).toString()
```

Most modern languages are strongly typed, but sometimes it is difficult to tell. Also, the definitions of strongly vs weakly typed languages are sometimes vague or not universally applied. That’s why this comparison is not used as often as dynamic vs static, which has a clearer set of rules.

## Dynamically typed vs statically typed

The difference between dynamically typed and statically typed languages is simply the difference between when the type is checked, either at runtime or compile time. A language enforcing data types will have a clear set of rules describing what input data types are expected, and what data type should be returned as a result of running the function.

With statically typed languages, checking types at compile time means the types are checked before the code is executed, meaning any type enforcement would be caught before a function is called. With dynamic languages, the type is checked at runtime, meaning only if and when a function is executed.

A lot of modern languages like ruby and python are dynamically typed. This makes for quicker delivery, but could cause errors to bubble up while the program is running, which could cause the program to crash if not properly anticipated. Being able to anticipate a potential error and placing error handling could lessen the risk here, but that also involves being able to anticipate what possible errors could be lurking in the code.

![typed-language-matrix](https://res.cloudinary.com/practicaldev/image/fetch/s--6V6DK8ku--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://miro.medium.com/max/1400/1%2ABddwVWW6hFU0miT9DCbUWQ.png)

## TypeScript

TypeScript is a superset of JavaScript, so if you know JavaScript, you are most of the way towards understanding TypeScript. In the above axis, TypeScript would fit into the quadrant that represents static and strong typed languages.

A key visual difference between TypeScript and JavaScript is that a TypeScript program has additional syntax to name the data types of inputs and outputs, as you would see in a programming language like Java or Swift, for example.

## Key Takeaways

* Strong vs weak - deals with whether data types are implicitly converted
* Dynamic vs static - deals with when the types are checked - at compile time or at runtime

## Exercise

* [W3 Schools TypeScript Tutorial](https://www.w3schools.com/typescript/)

## Additional Research

1. What is a strictly typed language?
2. What is duck typing?
3. What is nominal typing?
4. What is structural typing?

## Resources

* [Introduction to Static and Dynamic Typing](https://www.sitepoint.com/typing-versus-dynamic-typing/)
* [Magic lies here: Statically vs Dynamically Typed languages](https://medium.com/android-news/magic-lies-here-statically-typed-vs-dynamically-typed-languages-d151c7f95e2b)
* [What is the difference between runtime and compile-time?](https://www.educative.io/answers/what-is-the-difference-between-runtime-and-compile-time)
* [Statically Vs Dynamically Typed Languages (video)](https://www.youtube.com/watch?v=jlUZw8-6ljw)
* [TypeScript](https://www.typescriptlang.org/)
* [W3 Schools - TypeScript Tutorial](https://www.w3schools.com/typescript/index.php)

