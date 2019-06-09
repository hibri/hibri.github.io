---
title: The Testing Pyramid
layout: post
---

Any new change to the software we build has risk. To reduce/mitigate risk, we build quality into our software development process. Automated Tests are a fundamental part of building quality in. We can't deliver faster without the safety rails of automated testing. We need quick feedback on if we are building it right, and if we are building the right thing.

Different types of tests give us this quick feedback. We need to maintain the right combination of the different  test types. Doing so will help us to get the quick feedback and deliver faster.

For example; Focussing only on end to end testing may seem like getting more value for the effort spent. This is a common pattern at the start of projects. But, overtime maintaining end to end tests becomes a Sisyphean task. The effort is not worth the value.

We are building complex systems. A simple test strategy will not give us the confidence we need to go fast.

The Testing Pyramid is a visual metaphor to think about testing and the types of tests. This helps us communicate a test strategy.

![The Testing Pyramid](/public/images/2019-06-10-testing-pyramid.png)

Let's look at the different types of tests. We'll look at what each type of test should do. Let's also look at the effects of focussing on only one type of test and some of the common anti-patterns.

## Unit Tests
![Unit Tests](/public/images/2019-06-10-unit-tests.png)
Unit tests, test a unit of code. What is a unit of code? A class, a method? A couple of collaborating classes?  If it's a class do we test every method of a class?

A unit/class of code encapsulates behaviour and data. In unit testing we focus on testing behaviour. Not the implementation details. The [Single Responsibility Principle (SRP)](https://en.wikipedia.org/wiki/Single_responsibility_principle) states; 

"_Every module or class should have responsibility over a single part of the functionality provided by the software, and that responsibility should be entirely encapsulated by the class._"

If we follow SRP,  then the unit of code under tests, will have only a a couple of  methods as entry points. These methods provide access to the behaviour encapsulated by the class. (Large classes are code smells).  Unit tests exercise these methods. The test validates that the encapsulated behaviour is correct. We assert this in two ways. One, by asserting against the data returned. Two, by assert against the expectations on collaborating classes.

Unit tests should run fast (in milliseconds), in the same process and in-memory. Unit tests should not have any I/O or cross  any process boundaries. If or when they do they become another kind of test.

## Acceptance Tests

![Acceptance Tests](/public/images/2019-06-10-acceptance-tests.png)
Acceptance tests, test if we are building the right thing.  We write these tests in terms that our business and users can understand. With these tests we focus on only our code and the system we build. We mock out all the external dependencies. If we can't mock these out, we try to create local, in-memory or implementations that we can control.

For example if our system relies on a database, we hook it up to a lightweight version we can spin up in a container. An in memory version works even better (SQL-Lite, SQL Server Local edition). We can start our lightweight database from a clean, known state for our tests. We can through away the database after running tests, as no one else relies on it.

## Integration Tests

![Integration Tests](/public/images/2019-06-10-integration-tests.png)
Integration tests, test the code that integrates with other systems. This can be APIs built by another team, a database, a 3rd party integration. Anything that is outside of the code we own. Integration tests, test the boundaries of our code and the integration. These are different from end to end tests. 


## Monitoring and Alerts

![Monitoring and Alerts](/public/images/2019-06-10-monitoring+alerts.png)

Monitoring is based on things we know that could go wrong and have gone wrong in the past. The monitoring framework raises an alert when things go wrong with production systems.

I’ve included Monitoring and Alerting here because, we should know when [something is broken and why it’s broken](https://medium.com/@copyconstruct/monitoring-and-observability-8417d1952e1c). We should be alerted when something is already broken or is about to break. This shouldn’t be done as an after thought. 

Monitoring can be thought of as the [outer loop of TDD](https://benjiweber.co.uk/blog/2015/03/02/monitoring-check-smells/). 

## Smoke Tests

Smoke tests are a finger-in-the-air check whether the system is working. They test a happy path, or a critical path through the system. We should have only a few of these.

Smoke tests aren't intrusive. They aren't exhaustive either. Run them on production environments. We write smoke tests very early, when we build a walking skeleton of the system. This is a good time to start adding alerts.

## Manual Tests

![Manual Tests](/public/images/2019-06-10-manual-tests.png)
Manual tests are driven by a tester or a user. They are human driven. A tester interacts with the system as a user. Manual tests are costly, but valuable. Manual tests are the most expensive kind of tests, both in terms of money and effort. So we need to get the most value out of them.

Manual tests are valuable when they are exploratory tests. This is where we leverage the mindset of people who can break the system. If we lay the testing pyramid on it’s side, manual tests are the tip of the spear!! Manual tests explore the unknown.

The exploratory nature of these tests make them hard to automate. A repeated test belongs lower down the stack, where its automated. Manual tests explore the unknown. These tests look at the new capabilities of the system, and look at how users interact with the system in the wild. It's a process of converting the unknown unknowns into known unknowns.

## The Anti-Patterns and their effects

### Over-reliance on end to end (E2E) tests

End to end tests are an all-embracing simulation of real user scenarios. These tests are a symptom of  testing as an after thought. The myth is that this is where we get more value. E2E tests have value for very simple systems. As the system grows, there are more scenarios to test. The system grows in complexity.  E2E tests also reflect that complexity. The tests become fragile and take more time and effort to maintain. Spending this time and effort on unit tests is a better investment strategy.

E2E tests depend on all of the moving parts of a complex system being in the right state. The dependencies have to work perfectly. If another team breaks a dependent service, our tests will break. This makes E2E tests inherently fragile.

The only place we can get value out of E2E tests is in production, but then we are better off relying on our monitoring and alerts.

[Say no to More E2E Tests](https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html)

## Manual tests for each release

Doing manual tests only before each release is [release management theatre](https://continuousdelivery.com/2013/08/risk-management-theatre/).  This is wasteful. This anti-pattern is also the cause of the most common bottleneck to getting software released fast. The need to find someone to test before each release!

Tests before a release should be automated regression tests. If tests have passed earlier in the pipeline and we have confidence in them, then we shouldn’t need to test each release manually.

## Automated tests are the responsibility of the Automation QAs/Testers

When technology organisations start to do automated testing, the first thing they do is to recruit Automation Testers. This feeds the previous anti-pattern. 

Writing automated tests is a developer responsibility. Write the tests that prove the code works. 

When someone else writes the automated tests the developer doesn’t get feedback from the system they are building. The act of writing the automated test, gives the developer feedback on the system behaves in production. This feedback can be used to change the architecture of the system. 

Flaky tests can be fixed, as sometimes they point to a bug or to scalability constraint. A developer can bring in software engineering skills into the test codebase. Refactoring the test code can make tests more readable. Automated tests, that haven’t been written by a developer, tend to be a copy, pasted nightmare with timeouts all over the place. 

## Summary

It’s important that we get the balance between different types of tests right. We use our tests to give us early feedback. This is crucial, as we want to fail fast. When we rely on the wrong type of tests, feedback is delayed, or not present at all. Fast feedback is key to mitigating the inherent risk in the complex system we build. Without it we are building software blind. 

### Notes
1. A more detailed treatment of the testing pyramid. [The Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html) by Ham Vocke.
