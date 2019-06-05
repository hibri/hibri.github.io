# Testing Pyramids, Trophies, Diamonds and Doritos

Any new change to the software we build has risk. To reduce/mitigate risk, we build quality into our software development process. Automated Tests are a fundamental part of building quality in. We can't deliver faster without the safety rails of automated testing. We need quick feedback on if we are building it right, and if we are building the right thing.

Different types of tests give us this quick feedback. We need to maintain the right combination of the different  test types. Doing so will help us to get the quick feedback and deliver faster. 

For example; Focussing only on end to end testing may seem like getting more value for the effort spent. This is a common pattern at the start of projects. But, overtime maintaining end to end tests becomes a Sisyphean task. The effort is not worth the value.

We are building complex systems. A simple test strategy will not give us the confidence we need to go fast. 

The Testing Pyramid is a visual metaphor to think about testing and the types of tests. This helps us communicate a test strategy. 

Let's look at the different types of tests. We'll look at what each type of test should do. We'll also look at they all complement each other. Let's also look at the effects of focussing on only one type of test and some of the common anti-patterns.

## The Layers of the Pyramid

This is what the test pyramid describes. From bottom up.

Unit tests make up the bottom layer. Unit tests, test a unit of code. What is a unit of code? A class, a method? A couple of collaborating classes?  If it's a class do we test every method of a class?

A unit/class of code encapsulates behaviour and data. In unit testing we focus on testing behaviour. Not the implementation details. The [Single Responsibility Principle (SRP)](https://en.wikipedia.org/wiki/Single_responsibility_principle) states; 

"_Every module or class should have responsibility over a single part of the functionality provided by the software, and that responsibility should be entirely encapsulated by the class._"

If we follow SRP,  then the unit of code under tests, will have only a a couple of  methods as entry points. These methods provide access to the behaviour encapsulated by the class. (Large classes are code smells) .  Unit tests exercise these methods. The test validates that the encapsulated behaviour is correct. We assert this in two ways. One, by asserting against the data returned. Two, by assert against the expectations on collaborating classes. 

Unit tests should run fast, in the same process and in-memory.

Unit tests should not have any I/O or cross  any process boundaries. If/When they do they become another kind of test.

Next up the stack we have Integration and Acceptance tests. I want to be clear on what they mean.  Integration tests, test our code that integrates with other systems. This can be APIs built by another team, a database, a 3rd party integration. Anything that is outside of the code we own. Integration tests, test the boundaries of our code and the integration. These are different from end to end tests. I'll describe this later.

Acceptance tests, test if we are building the right thing.  We write these tests in terms that our business and users can understand. With these tests we focus on only our code and the system we build.  Not the external dependencies. We mock out all these external dependencies. If we can't mock these out, we try to create local, in-memory or implementations that we can control. 

For example if our system relies on a database, we hook it up to a lightweight version we can spin up in a container. An in memory version works even better (SQL-Lite, SQL Server Local edition). We can start our lightweight database from a clean, known state for our tests. We can through away the database after running tests, as no one else relies on it.

Next up in the stack, we have monitoring and alerting. This is based on things we know that could go wrong and have gone wrong in the past. The monitoring framework raises an alert when things go wrong with production systems.

Next up in the stack, we have our smoke tests. Smoke tests are a finger-in-the-air check of if the system is working. They test a happy path, or a critical path through the system. We should have only a few of these. Not too many. Smoke tests aren't intrusive. They aren't exhaustive either. Run them on production environments. We write smoke tests very early, when we build a walking skeleton of the system. This is a good time to start adding alerts. 

Next up the stack, we have our manual tests. These are exploratory tests. This is where we leverage the mindset of people who can break the system.

The exploratory nature of these tests make them hard to automate. A repeated test belongs lower down the stack, where it's automated. Manual tests explore the unknown. These tests look at the new capabilities of the system, and look at how users interact with the system in the wild. It's a process of converting the unknown unknowns into known unknowns. 

## The Anti-Patterns and their effects.

### Over-reliance on end to end (E2E) tests

End to end tests are an all-embracing simulation of real user scenarios. These tests are a symptom of  testing as an after thought. The myth is that this is where we get more value. E2E tests have value for very simple systems. As the system grows, there are more scenarios to test. The system grows in complexity.  E2E tests also reflect that complexity. The tests become fragile and take more time and effort to maintain. Spending this time and effort on unit tests is a better investment strategy.

The only place we can get value out of E2E tests is in production. 

([https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html)](https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html)

## Manual tests for each release

Doing manual tests only before each release is an anti-pattern. There is more value in manual tests when they are done all the time.