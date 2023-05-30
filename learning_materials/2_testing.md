# Testing

## Course Goals

* Name the four sequential phases of a test
* Write a unit test using the four phases
* Describe the testing pyramid and how each type of test is used within an application
* Outline and describe the three rules of test-driven development
* Describe some of the benefits and costs of test-driven development
* Define the term "refactoring" and describe how it fits into the TDD cycle

## Summary

Well tested software is important because it enables developers to make changes to a code base without fear of breaking the code already implemented. Software can change for many reasons, and having a well tested code base provides confidence that refactoring will not change the existing behavior.

Tests also serve as a type of documentation for the code, a contract to provide assurance about the behavior of the code. A contract that can be asserted, simply by running the test suite.

Another benefit of testing is that it can help to inform the design of your application. Particularly with test-driven development (TDD), testing helps to identify the dependencies of each component, which in turn helps in driving the design and shape of the application, thus informing when certain complexity should be abstracted.

## Four-Phase Test

The “four phase test” refers to a common pattern in which unit tests are structured. The four phases are setup, exercise, verify, and teardown.

### Setup
The setup phase of a test involves setting the stage to mimic the conditions in which the test should be run. This includes creating and setting up the class where the behavior resides, and providing any input necessary for the function.

Let’s say, for example, we are testing the behavior of an animal class. The animal class requires some input to inform the “shape” of the animal. Let’s say, for instance, you want to specify that the animal is a cat, and the cat’s name is “Phillip”. Your test set up would look like this:

```java
cat = Animal(type: ‘cat’, name: ‘Phillip’)
```

### Exercise
The exercise phase simply refers to calling the particular function on the class that you created in the setup phase.

In the animal example, let’s say we want to have the cat make a noise. The setup phase would be calling the method that would provide that functionality.

```java
sound = cat.makeNoise()
```

### Verify
During the verify phase of a unit test, we make assertions about the behavior that we expect to happen as a result of calling the method in the exercise phase.

```java
assertEqual ‘meow’, sound
```

### Teardown

The final phase of a unit test is the teardown, where the system is reset to its pre-test phase. This could be where you rollback a database transaction, or perhaps to remove temporary files that were created as a result of the code execution.

The teardown is usually an implicit responsibility of the testing framework, so you may not need to actually do anything for this step. Pytest does have a `tearDown()` method that can be overwritten if there are specific behaviors you want to occur after each test.

## Testing Pyramid

![Testing pyramid](https://martinfowler.com/bliki/images/testPyramid/test-pyramid.png)

The testing pyramid is a concept that depicts three types of tests that should be included in a test suite, their cost relative to each other, and the time they take to execute.

### Unit Tests

Unit tests are automated and represent smaller, more isolated pieces of the code. They are faster to run and have a lower development and execution cost than tests higher on the pyramid, which are not usually automated and have a much larger cost associated.

Because unit tests represent smaller chunks of the code, there will be a greater quantity of them. They should not rely on external dependencies; dependencies should be mocked or stubbed to keep the test isolated and scope small.

### Integration Tests

The next level of test, integration tests, will test the behavior of larger chunks of the code. These tests will test how parts of code interact with each other. These tests have a higher cost than unit tests because they tend to be slower, as they are actually connecting to both different parts of the codebase and external services. These external interactions may include connecting to a database, external APIs, or other web services, calls that a unit test would mock out.

### UI Tests

UI tests, also known as end-to-end tests or user acceptance tests, involve testing through a user interface. Typically these tests would be manually run by QA team members, as they take a lot of time and require more effort. Consequently, they are much more expensive to run and will be less numerous.

UI testing takes into consideration the many different ways that a user can interact with the application, and what could potentially go wrong. This is also where the application would be tested on real devices and across different browsers to ensure that the code is working properly under real life scenarios.

## Test-Driven Development

Test-driven development is a methodology of writing tests where the tests are written before the code that would implement the functionality being tested. The tests serve to verify the behavior, so writing the tests before the code is written helps to define the design of the code.

### Red, Green, Refactor

The three rules or phases of test-driven development are red, green, refactor.

![Red, Green, Refactor](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*tZSwCigaTaJdovyWlp5uBQ.jpeg)

#### Red

The red phase refers to writing the unit test, running the test, and watching it fail. The test will fail because you have not yet written the functionality to make the test pass.

#### Green

The green phase involves writing the code to make the code pass. This could be as simple as explicitly returning the exact value you expect to see.

For example, say we are dealing with a program that converts an Arabic number to a Roman numeral. One of the first baseline test cases we would deal with is converting the number 1 to a roman numeral I. Simply returning I in the convert method would satisfy this requirement, but future test cases would fail (ie: if we passed in 2, the method explicitly returning I will fail the assertion).

#### Refactor

The refactor phase is where we want to refine the method to make it reusable for multiple test cases.

In the Roman numerals example, we may want to change our method to accept values higher than 1. The next simplest test case would be to test for 2. In that case, we could return I times the input number. That will only work for values 1-3, but we have not yet written the test case for the higher values, so we can defer implementing that functionality until we need it.

### Benefits and Costs of TDD

*source [What are the costs and benefits of TDD?](https://practicingruby.com/articles/tdd-costs-and-benefits)*

#### Benefits
* Increased confidence in developers working on test-driven codebases
* Increased protection from defects, especially regressions
* Better code quality (in particular, less coupling and higher cohesion)
* Tests as a replacement/supplement to other forms of documentation
* Improved maintainability and changeability of codebases
* Ability to refactor without fear of breaking things
* Ability of tests to act as a "living specification" of expected behavior
* Earlier detection of misunderstandings/ambiguities in requirements
* Smaller production codebases with more simple designs
* Easier detection of flaws in the interactions between objects
* Reduced need for manual testing
* Faster feedback loop for discovering whether an implementation is correct

#### Costs
* Slower per-feature development work because tests take a lot of time to write
* Steep learning curve due to so many different testing tools / methodologies
* Increased cost of test maintenance as projects get larger
* Some time wasted on fixing "brittle tests"
* Effectiveness is highly dependent on experience/discipline of dev team
* Difficulty figuring out where to get started on new projects
* Reduced ability to quickly produce quick and dirty prototypes
* Difficulty in evaluating how much time TDD costs vs. how much it saves
* Reduced productivity due to slow test runs
* High setup costs

## Exercises
* TDD TypeScript FooBar
* [Pokemon API Client - Day 1](https://github.com/fravila08/pokemonEx/tree/main/exercise_1

## Resources

* [Fundamentals of TDD (video)](https://thoughtbot.com/upcase/fundamentals-of-tdd)
* [The Three Rules of TDD](http://butunclebob.com/ArticleS.UncleBob.TheThreeRulesOfTdd)
* [Red, Green, Refactor](https://www.codecademy.com/article/tdd-red-green-refactor)
* [Characteristics of a Good Test](https://www.codecademy.com/article/tdd-u1-good-test)
* [The Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html)
* [Test with Mock Objects](https://martinfowler.com/articles/mocksArentStubs.html)
* [Test Smells](https://testsmells.org/)
* [Growing Object-Oriented Software, Guided By Tests (book)](https://www.amazon.com/Growing-Object-Oriented-Software-Guided-Tests/dp/0321503627)
* [Getting Started With Testing in Python](https://realpython.com/python-testing/)
* [What are the costs and benefits of TDD?](https://practicingruby.com/articles/tdd-costs-and-benefits)
