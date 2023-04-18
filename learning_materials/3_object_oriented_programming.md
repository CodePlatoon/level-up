# Object Oriented Programming

## Course Goals

* Explain the attributes of OOP
  * encapsulation
  * composition
  * inheritance
  * abstraction
  * polymorphism
* Explain how functional programming and procedural programming differ from object oriented programming
* Describe the SOLID principles
  * Single Responsibility Principle
  * Open-closed Principle
  * Liskov Substitution Principle
  * Interface Segregation Principle
  * Dependency Inversion Principle

## Summary

Object Oriented Programming (OOP) is a commonly used paradigm of software design that centers the design around the concept of “objects”. An object in programming terms is composed of functions (code that performs an action), and attributes (data). OOP focuses on reusability and modularity.

Other types of software design paradigms include functional programming (FP) and procedural programming. OOP is a common choice for modern software development because it simplifies many programming problems. It is considered easier to learn because it models code in a way that is similar to how objects exist in the real world.

Many modern programming languages, like Python and Ruby, are designed as OOP languages and are well suited for beginner learners.

## Attributes of Object Oriented Programming

### Encapsulation
Encapsulation involves creating self-contained modules that bundle data and methods to work within a single unit. The unit also hides the state of the unit from the outside. A key benefit to hiding state and data from outside objects is that it prevents external APIs or scripts from accessing the code within the module.

### Composition
Composition describes a class that references one or more objects of other classes through instance variables. In composition, one class “has-a” relationship with another class. Composition allows you to reuse code by enabling you to build complex objects composed of other objects. For example, a computer is composed of many components that could be taken out and reused in other computers.

### Inheritance
Classes are created in hierarchies. Inheritance allows the structure and methods in one class to be passed down the hierarchy to sub-classes. This means that you can reuse code of classes that are inherited from. Inheritance differs from composition because a class that inherits from another “is-a” version of the higher up class. For example, a motorcycle “is-a” vehicle, as is a car. They both have attributes of a vehicle, yet they are very different.

### Abstraction
Abstraction handles complexity by hiding details from the user. APIs are a good example of an abstraction layer. With an API, you make a call to a method and then the method works behind the scenes to process your request.

### Polymorphism
Polymorphism refers to an object, data, or function to be able to take on multiple forms. For instance, two classes that are within the same hierarchy may have a method that has the same name, but operates completely differently. An example of this would be with a parent class of animal. You can have a method called makeNoise() that would meow for a cat and bark for a dog.

## OOP vs other programming paradigms

Solving problems with code can be accomplished in many different ways. Three common paradigms are FP, procedural programming, and OOP. Each has its advantages and disadvantages.

Functional Programming
Functional programming (FP) works in a completely different way than OOP. With FP, you don’t have the concept of objects. Instead, a functional language relies on methods (functions) that don’t rely on any external mutable state like global variables. Defined variables in functional programming cannot change their values. If additional values are needed, a new variable would need to be created.

The functions have clearly defined inputs and outputs, and instead of changing existing data, the functions always return new data. With functional programming, there are no side effects to the functions; given the same input to a function, the output will always be the same.

Code with immutable data and without side effects makes it much more difficult to introduce bugs into the code, and if a problem does occur, it is a lot easier to catch because you don’t have to consider data transformation as a possible suspect.

A functional programming language is often a great choice for parallel programming over OOP because they don’t deal with state changes, so the code is highly efficient. Another benefit is reusability of the code–because immutable data is easy to test, compose, move, and reuse, modules can easily be moved around and reused throughout the codebase.

Some common functional programming languages include Clojure, Elixir, Haskell, and Scala.

Procedural Programming

Procedural programming is linear programming; it takes a top-down approach. Procedures, or routines, are a series of computational steps that are to be carried out. Programming in a procedural way, like writing scripts, for example, is pretty straightforward because there is no framework involved and few design concepts to have to learn.

With procedural programming, there is no concept of hiding data, so it is less secure. Also, making changes in procedural programming can be difficult because there are no mechanisms for code reuse as there are in OOP.

Early programming languages like FORTRAN, COBOL, BASIC, Pascal and C are procedural programming languages.

## SOLID Principles

The SOLID Principles are a set of design principles used in OOP. They are considered best practices for designing object oriented programs.

### Single Responsibility Principle

The Single Responsibility Principle (SRP) highlights the idea that a class should, as the name suggests, be responsible for one thing only. Modules that follow this principle have code that is highly cohesive, meaning the behaviors are highly related and strongly focused.

A good barometer as to whether a class is following this principle is if, when describing the functionality of the class, you say “and”, it probably is not following the single responsibility principle. For instance, a class should not both read from an input source and write to an output source. These responsibilities should be split into two separate classes. A class called LightSwitch should be able to go from on to off. It shouldn’t be able to change the bulbs or control electricity. Alternatively, a class that is getting user input should not do anything with that input.

One of the benefits of keeping highly cohesive, single responsibility classes is that when alteration happens, the class that needs to be changed is isolated, decreasing the likelihood that breakage would occur in other unrelated parts of the code. Additionally, SRP classes are usually easier to understand because there are usually fewer methods that are self explanatory. Also, single responsibility classes are reusable in that, if a class does multiple things, but only one of the things is necessary in another part of the software, then the extra responsibilities are going to be a hindrance.

> _A class or module should have one, and only one, reason to change_

Besides talking about classes doing one thing, you should also consider the definition of the single responsibility, in that the class should only have one reason to change. A reason to change is the responsibility.

Let’s look at an example of a single responsibility principle violation:

```java
class Person {
    let firstName: String
    let lastName: String
    let email: String

    init(firstName: String, lastName: String, email: String) {
        self.firstName = firstName
        self.lastName = lastName
        self.email = validateEmail(email)
    }

    func validateEmail(email : string) -> String {
        let regex = NSRegularExpression(pattern: "^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$", options: .CaseInsensitive, error: nil)
        if (return regex?.firstMatchInString(self, options: nil, range: NSMakeRange(0, countElements(self))) != nil) {
            return email
        } else {
            // handle invalid email
        }
    }

    func sayHi() {
        print("Well hello there, \(firstName) \(lastName). I am sending you an email to \(email).")
    }
}
```


Here there is a person class, but in addition to the person class having the responsibility of greeting a person, it is also validating the email. These are two distinct responsibilities. To fix this, we can pull the functionality of the email validation into an email class:

```java
extension String {
    func isValidEmail() -> Bool {
        let regex = NSRegularExpression(pattern: "^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$", options: .CaseInsensitive, error: nil)
        return regex?.firstMatchInString(self, options: nil, range: NSMakeRange(0, countElements(self))) != nil
    }
}

class Email {
    var email: String

    init(email: String) {
        self.email = validateEmail(email)
    }

    func validateEmail(email: String) -> String {
        if email.isValid? {
            return email
        } else {
            // handle invalid email
        }
    }
}
```

We have removed the responsibility of the Person class to validate the email address by creating a new Email class that knows how to validate itself. Now we can use dependency injection to supply the Person class with a valid email. Now, if for some reason we have to change the way that the email is handled or input, we only have to change the Email class and not the Person class. Similarly, changes to the Person class should not handle the way that Email works.

### Open-closed Principle

The Open-Closed Principle (OCP) states that

> _“software entities should be open for extension, but closed for modification”._

What exactly does that mean?

One way that you can think about OCP is that in order to make modifications, you are not actually changing a base class, but rather, you are adding code in the form of an abstraction to deal with the new requirements. This is easier to illustrate with an example.

Let’s take into consideration estimating the area of multiple shapes.

We can demonstrate this principle by calculating the total area of multiple rectangles by adding the area of each rectangle together. For this we would need a rectangle object that defines two values, length and width.

```java
class Rectangle
{
  var length: Float
  var width: Float

  init(length: Float, width: Float) {
    self.length = length
    self.width = width
  }
}
```

In order to calculate the total area, we could use a  ShapeAreaCalculator to calculate the area of each individual rectangle object and sum those together.

```java
class ShapeAreaCalculator
{
  func calculateArea(rectangles: [Rectangle]) -> Float {
    area: Float = 0
    for rectangle in rectangles {
      area += rectangle.width * rectangle.height
    }
    return area
  }
}
```

#### Problem

But wait, we did not consider our circles. They have their own struct that considers a circle’s radius along with the constant of PI. If I want to figure in circles, I have to modify the ShapeAreaCalculator class, which is a violation of the closed to modification rule of OCP. I am adding methods to calculate each shape’s individual area, and changing the guts of the calculateArea() function entirely:

```java
func calculateArea(rectangles: [Rectangle], circles: [Circle]) -> Float {
  area: Float = 0
  area += Float(calculateRectangleArea(rectangles))
  area += Float(calculateCircleArea(circles))
  return area
}
```

Now another shape pops up: a trapezoid. Now I have to add a Trapezoid class, which is not a big deal, but I also have to modify my class by adding another method call in the calculateArea() method, as well as the extra method now being called.

```java
func calculateArea(rectangles: [Rectangle], circles: [Circle], trapezoids: [Trapezoid]) -> Float {
  area: Float = 0
  area += calculateRectangleArea(rectangles)
  area += calculateCircleArea(circles)
  area += calculateTrapezoidArea(trapezoids)
  return area
}
```

As you can see, modifying the class every time I need to add a new shape is not very efficient. Every time I change the class, I have to recompile, which affects other modules that depend on this class. Sure, on this scale, it may not seem like a huge deal, but no example will be this small in real life.

#### Solution
A way to solve this that would not be in violation of OCP would be through use of abstractions. I can create a Shape abstraction that each of the shape types can adopt. I am going to make a Shape protocol that requires the calculateShapeArea() function in each adopting class.

```java
protocol Shape {
  func calculateShapeArea()
}
```

Now I have to redesign my rectangle, circle and trapezoid classes to adopt this protocol. In order for each to conform to the new protocol, each has to include the calculateShapeArea() function.

```java
class Rectangle : Shape
{
  var length: Float
  var width: Float

  init(length: Float, width: Float) {
    self.length = length
    self.width = width
  }

  func calculateShapeArea() {
    return width * height;
  }
}
```

Now when we call on the ShapeAreaCalculator class to give us a total area, the type of shape that is being used in the calculateArea() method does not matter because each individual shape is handling the calculation of its own area.

```java
class Shape AreaCalculator {
  func calculateArea(shape: [Shape]) -> Float {
    area: Float = 0
        for shape in shapes
          area += shape.calculateShapeArea();
        }
    return area;
  }
}
```

### Liskov Substitution Principle

> _Let q(x) be a property provable about objects x of type T. Then q(y) should be provable for objects y of type S,where S is a subtype of T._

The above definition of the LSP is pretty math-heavy. Thankfully, there is this alternative definition:

> _If a program module is using a Base class, then the reference to the Base class can be replaced with a Derived class without affecting the functionality of the program module_

Essentially what this means is that subtypes must be substitutable for their base types.

It may be hard to grasp the difference between a sub-type and a base type. A sub-type is the class or object that inherits from the base class. A base is the original and the sub is what is derived from the base. You can also say that the sub extends the base.

Let’s consider a car as a base type. We know that the vehicle has an engine, a battery, and that it drives. We also know that it accepts fuel of some type.

```java
class Car {
    var hasEngine: Bool
    var hasBattery: Bool

    func Drive() {
        // code to make it drive
    }

    func refuel() {
        // code to refuel
    }
}
```

Now let’s say that we are working with a fancy future car that is a subtype of vehicle. This car still has an engine and a battery, still drives. The future car still needs fuel. Therefore we can safely say that a FutureCar is a subtype of Car. Right?

Not so fast. Let’s think about one aspect of a car, refueling. For the base class of Car, the fuel is given in terms of a liquid to a fuel tank from which the engine feeds. But with FutureCar, the fuel that it is receiving is in the form of solar rays converted to energy.

![Future Car](https://www.iar.com/siteassets/about/customers/stanford-solar-car-project/solarfull.png)

The `refuel()` function in both classes is not, in fact, the same. A future car could not be substituted for a Car because neither would not satisfy the other’s energy acquisition requirements.

Another problem that we face is that there is also a violation of the Open-Closed Principle because our base class, car, cannot be extended. When we specified the method of refueling, we broke that.

One thing that we could do in order to ensure that we are not violating the Liskov Substitution Principle is to use interfaces and protocols as contracts. This is a pattern called, not coincidentally, design by contract. It is a way of determining formal specifications by which types adopting the “contract” must abide.

In the case of the Car and FutureCar, this would not have helped exactly because both instances use an interpretation of the refuel() function. We could, however, bind the two more securely by specifying the type of fuel as an input for the function.

The bottom line is, sometimes when we think that something passes the “is-a” test in real life (a future car is a car, a square is a rectangle), consider whether the design of your code complements that reality. Many times things hold true in the real world, but those ideas fall apart when broken down in code.

### Interface Segregation Principle

The segregation part of interface segregation is pretty simple to understand. We want our interfaces to work independently of other parts of the system. We can also deduct that this means that the interfaces will be free of dependencies.

Then we have an interface. You can think of an interface as the part of something with which a user interacts. For instance, the physical interfaces you have with your computer include your mouse, your keyboard, and the power button. With your cell phone (mini-computer), you interact with the different buttons (power, volume), as well as the touch screen, speakers and headphone jack. You can interact with your phone by pressing the buttons to control the volume, or by plugging in external speakers to jam out to some epic 90’s alternative rock.

The Interface Segregation Principle is a means to keep polluted data and functionality from your interfaces (fat interfaces). Interfaces should only include the data that is necessary for the client to interact. We would not want to have an extra set of Korean letter buttons on our keyboard if we never use them. There should be separate keyboards for those who want to type in Korean versus those who want to type in English.

Also, it would be very wasteful to add functionality to the interface that does not do anything to change the object to which it is paired. Generally, our cell phones should not control our vacuum cleaner or our treadmill. These devices should have their own specialized interfaces. Being able to control a treadmill’s speed from your phone, while this may seem practical, serves no benefit to the phone itself.

> _Clients should not be forced to implement interfaces they don’t use_

When you have an interface that has low cohesion, it is difficult to reuse in other parts of the code. As with classes, interfaces that have unrelated methods should be split. Say you have the following protocol for bookkeeping.

```java
protocol KeepsBooks {
    func calculateBalance()
    func calculateMonthToDateBalance()
    func addCredit()
    func addDebit()
}
```

Everything is accounting-centric. These are all tasks that have to do with bookkeeping. But what if we wanted a BalancePrinter of some sort to adopt this protocol? Our balance printer would be forced to use the addCredit() and addDebit() functions, even if they are void of logic. This does not make sense. A more sensible approach would be to split the KeepsBooks protocol into two separate protocols that handle the functions separately.

The lesson here is that clean, organized code does not stop with small methods and classes. Our interfaces should also be focused so that we can reuse them without needing to implement unnecessary functionality.

### Dependency Inversion Principle

When thinking about the idea of Dependency Inversion, it helps to think of real-world, concrete examples.

John Sonmez, on his website Simple Programmer, explains that you can consider all of your home portable electronics for a real life violation of the Dependency Inversion Principle. Each item, like a cell phone, wireless headphones, and a video game controller, has to interact with the house in order to get electricity to recharge its associated battery. The interface between the house and the device is the charger.

The reason that this violates the Dependency Inversion Principle is because each device is dictating to the house how it will be charged, rather than the house telling the devices how it will charge them. “Your home’s charging capability should define the interface the devices have to use”. The dependency for the interface should be defined by the house; it should be inverted.

One example of a properly inverted dependency would be the DMV in some cases. The DMV requires all who want to acquire a driver’s license to fill out the same forms. It is setting the contract that those who depend on the DMV have to follow. The DMV would not accept a handwritten piece of paper with the same information; they only accept DMV forms for the service requested.

## Exercise

* [Pokemon API Client - Day 2](https://github.com/fravila08/pokemonEx/tree/main/exercise_2)

## Resources

* [Object Oriented Programming Concepts](https://www.freecodecamp.org/news/object-oriented-programming-concepts-21bb035f7260)
* [Object Oriented Programming Tricks](https://hackernoon.com/oo-tricks-the-art-of-command-query-separation-9343e50a3de0?ref=hackernoon.com)
* [GORUCO 2009 - SOLID Object-Oriented Design by Sandi Metz](https://www.youtube.com/watch?v=v-2yFMzxqwU&t=2s)
* [Growing Object-Oriented Software, Guided By Tests (book)](https://www.amazon.com/Growing-Object-Oriented-Software-Guided-Tests/dp/0321503627)
* [SOLID Object-Oriented Design by Sandi Metz (video)](https://www.youtube.com/watch?v=v-2yFMzxqwU)
* [SOLID Principles: Explanations and Examples](https://itnext.io/solid-principles-explanation-and-examples-715b975dcad4)
* [SOLID fun explanations with images](https://imgur.com/gallery/CgWZFId)
* [LSP Explained](https://reflectoring.io/lsp-explained/)
* [Simple Programmer](https://simpleprogrammer.com/)
