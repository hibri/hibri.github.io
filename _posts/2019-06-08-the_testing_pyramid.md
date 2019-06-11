---
title: The Testing Pyramid
layout: post
author: Hibri Marzook
published: true
date: 2019-06-10T20:00:00+00:0

categories:
  - Continuous Delivery
  - Contiunous Integration
  - Devops
  - TDD
  - Agile

tags:
  - continous-delivery
  - devops
  - tdd


---

Any new change to the software we build has risk. To reduce risk, we build quality into our software development process. Automated Tests are a fundamental part of building quality in. We need to build quality in order to go faster. Automated tests  are the safety rails that allow us to go faster. Automated tests provide the crucial quick feedback on if we are building it right and if we are building the right thing, as we go faster. 

Different types of tests are needed to give fast feedback and we need to maintain the right balance of the different types of tests. Getting this balance right helps get fast feedback, to deliver faster.

For example; Focussing on end to end testing provides the illusion of more value for the effort spent, at the start of a project. But, overtime maintaining end to end tests is a Sisyphean task, diminishing  the value we get out of E2E tests.

We are building complex systems. Our tests mirror the systems we build. A simple and singular test strategy will not give us the confidence we need to go fast.

The Testing Pyramid is a visual metaphor to think about testing and the types of tests. This helps us communicate a test strategy. It acts as a guide to getting the balance of the different types of tests right.

![The Testing Pyramid](/public/images/2019-06-10-testing-pyramid.png)

Let's look at the different types of tests. We'll look at what each type of test should do. Let's also look at the effects of focussing on only one type of test and some of the common anti-patterns.

## Unit Tests

![Unit Tests](/public/images/2019-06-10-unit-tests.png)

Unit tests, test a unit of code. What is a unit of code? A class, a method? A couple of collaborating classes?  If it's a class do we test every method of a class?

A unit of code encapsulates behaviour and data. In unit testing we focus on testing behaviour. Not the implementation details. The [Single Responsibility Principle (SRP)](https://en.wikipedia.org/wiki/Single_responsibility_principle) states; 

"_Every module or class should have responsibility over a single part of the functionality provided by the software, and that responsibility should be entirely encapsulated by the class._"

If we follow SRP, then the unit of code under test, will have only one method (or two) as an entry point. The entry point provides access to the behaviour encapsulated by the unit of code. Unit tests exercise these. The test asserts that the encapsulated behaviour is correct. 

We assert this in two ways. First, by asserting against the data returned. Second, by asserting against the expectations against collaborating classes.

Unit tests should run fast (in milliseconds), in the same process and in-memory. Unit tests should not have any I/O or cross  any process boundaries. If they do, then they become another kind of test.

## Acceptance Tests

![Acceptance Tests](/public/images/2019-06-10-acceptance-tests.png)

Acceptance tests, test if we are building the right thing.  We write these tests in terms that our business and users can understand. With these tests we focus on only our code and the system we build. We mock out all the external dependencies. If we can't mock these out, we try to create local, in-memory or implementations that we can control.

For example if our system relies on a database, we hook it up to a lightweight version we can spin up in a container. An in memory version works even better (SQL-Lite, SQL Server Local edition). We can start our lightweight database from a clean, known state for our tests. We can through away the database after running tests, as no one else relies on it.

## Integration Tests

![Integration Tests](/public/images/2019-06-10-integration-tests.png)

Integration tests, test the code that integrates with other systems. This can be APIs built by another team, a database, a 3rd party integration. Anything that is outside of the code we own. Integration tests, test the boundaries of our code and the integration. These are different from end to end tests. 


## Monitoring and Alerts

![Monitoring and Alerts](/public/images/2019-06-10-monitoring+alerts.png)

Monitoring is based on things we know that could go wrong and have gone wrong in the past. The monitoring  and alerting framework raises an alert when things go wrong with the production system.

I’ve included Monitoring and Alerting here because, we should know when [something is broken and why it’s broken](https://medium.com/@copyconstruct/monitoring-and-observability-8417d1952e1c). We should be alerted when something is already broken or is about to break. This shouldn’t be done as an after thought. We should test or alerts even in test environments. Consider adding alerts to the [walking skeleton](https://wiki.c2.com/?WalkingSkeleton).

Monitoring can be thought of as the [outer loop of TDD](https://benjiweber.co.uk/blog/2015/03/02/monitoring-check-smells/). 

## Smoke Tests

Smoke tests are a finger-in-the-air check whether the system is working. They test a happy path, or a critical path through the system. We should have only a few of these.

Smoke tests aren't intrusive. They aren't exhaustive either. Focus on critical user journeys. Run them on production environments. We write smoke tests very early, when we build a walking skeleton of the system.

## Manual Tests

![Manual Tests](/public/images/2019-06-10-manual-tests.png)
Manual tests are driven by a tester or a user. They are human driven. A tester interacts with the system as a user. Manual tests are costly, but valuable. Manual tests are the most expensive kind of tests, both in terms of money and effort. So we need to get the most value out of them.

Manual tests are valuable when they are exploratory tests. This is where we leverage the mindset of people who can break the system.

![Unknown and known risks](/public/images/2019-06-10-manual-unknown-risks.png)

Manual tests explore the unknown. These tests look at the new capabilities of the system. They look at how users interact with the system in the wild. It's a process of converting the unknown unknowns into known knowns. We can only automate against expected states we know.

## The Anti-Patterns and their effects

### Over-reliance on end to end (E2E) tests

End to end tests are an all-embracing simulation of real user scenarios. An over-abundance of these tests are a symptom of testing as an after thought. The myth is that this is where we get more value. E2E tests have value for very simple systems. 

As the system grows, there are more scenarios to test. The system grows in complexity.  E2E tests reflect that complexity. The tests become increasingly fragile and take more time and effort to maintain. Spending this time and effort on unit tests is a better investment strategy.

E2E tests depend on all of the moving parts of a complex system being in the right state. The dependencies have to work perfectly. If another team breaks a dependent service, our tests will break. This makes E2E tests inherently fragile.

The only place we can get value out of E2E tests is in production, but then we are better off relying on our monitoring and alerts.

[Say no to More E2E Tests](https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html)

## Manual tests for each release

Doing manual tests only before each release is [release management theatre](https://continuousdelivery.com/2013/08/risk-management-theatre/).  This is wasteful. This anti-pattern is also the cause of the most common bottleneck to getting software delivered fast.

Tests before a release should be automated regression tests. If tests have passed earlier in the pipeline and we have confidence in them, then we shouldn’t need to test each release manually.

## Automated tests are the responsibility of the Automation QAs/Testers

When technology organisations start to do automated testing, the first thing they do is to recruit Automation Testers. This feeds the previous anti-pattern. 

I’ve seen test code rot due to the lack of maintenance, because they are owned by the “Automation QAs”. No one fixes the slow or flaky tests. Eventually the build is red all the time, and someone turns off the tests, saying “Automated testing doesn’t work for us”.

![This is fine](/public/images/2019-06-10-this-is-fine.png)

Writing automated tests is a developer responsibility. Write the tests that prove the code works. 

When someone else writes the automated tests the developer doesn’t get feedback from the system they are building. The act of writing the automated test, gives the developer feedback on how the system behaves in production. This feedback can be used to change the architecture of the system. 

Flaky tests can be fixed, as they could point to a bug or to scalability constraint. A developer can bring in software engineering skills into the test codebase and refactoring the test code to make it more readable. 

Automated tests, that haven’t been written by a developer, tend to be a copy, pasted nightmare with scattered timeouts.

## Summary

It’s important that we get the balance between different types of tests right. We use our tests to give us early feedback. 

This is crucial, as we want to fail fast. When we rely on the wrong type of tests, feedback is delayed, or not present at all. Fast feedback is key to mitigating the inherent risk in the complex system we build. Without it we are building software blind. 

### Notes
1. A more detailed treatment of the testing pyramid. [The Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html) by Ham Vocke
2. I also like the [Small, Medium and Large nomenclature](https://testing.googleblog.com/2010/12/test-sizes.html) for tests bu Simon Stewart
