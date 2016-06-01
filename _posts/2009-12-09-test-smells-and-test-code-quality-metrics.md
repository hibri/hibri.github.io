---
id: 316
title: Test Smells and Test Code Quality Metrics
date: 2009-12-09T22:15:58+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2009/12/09/TestSmellsAndTestCodeQualityMetrics.aspx
permalink: /2009/12/09/test-smells-and-test-code-quality-metrics/
categories:
  - Agile
  - development
  - TDD
---
The major highlight at XP Day 2009, was <a href="http://gojko.net/2009/12/07/improving-testing-practices-at-google/" target="_blank">Mark Striebeck’s talk on unit testing practices at Google</a>.&#160; What makes a good test depends on experience , skill and school of thought. I had to agree when he said that developers can be almost religious when it comes to the topic of what makes a good test. This made them solve this problem the Google way, by gathering data. Let the data speak. 

He went on to describe metrics that they were collecting on tests and test code.&#160; A test that has never failed is likely to be a bad test. If the test was fixed to make the test pass, then this is also an attribute of a bad test. A test can be a good test if the code was fixed to make the test pass.

This got me thinking. Generally I haven’t gathered metrics on test code. We have a pretty good <a href="http://blog.robbowley.net/2009/10/28/visualising-the-internal-quality-of-software-part-1/" target="_blank">metrics dashboard</a> for production code. What metrics can I gather on test code ? 

Metrics on test code should also focus on the readability of the code. Having large test methods is ok, but not too big. My opinion is that a test method with more than 20 lines is too big. 

Tests should be concise, the assert should be obvious. Some code duplication is fine to make the test readable. This is all fine, but how can I get these as metrics&#160; ? Only way to judge this is to eyeball the tests, and there are differences of opinion. 

However, there are ways to measure what a test should not be. These are test smells. Test smells are described in <a href="http://www.amazon.co.uk/gp/product/0131495054?ie=UTF8&tag=hibrinet-21&linkCode=as2&camp=1634&creative=19450&creativeASIN=0131495054" target="_blank">xUnit Test Patterns</a>

I’ve listed a few test smells and <a href="http://www.ndepend.com/Metrics.aspx" target="_blank">NDepend CQL queries</a> find these smells. These can be automated in the build process and flagged up.

**Large Test Methods**

These can be a chore to read. Tests should be written as simply as possible. These also&#160; point to too many responsibilities and dependencies in the code being tested, as most of the test code is used to do setup for the test.

_SELECT METHODS WHERE HasAttribute "NUnit.Framework.TestAttribute" AND&#160; NbLinesOfCode > 20_

**Large setup methods**

Usually when unit testing the same code, we tend to have a common setup method, in order to make the test more readable. What happens is, more and more code is moved into the common setup method. We get blind to this after a while, and all the dependencies for the test are hidden away. If you do have [Setup] methods, keep them small.

_SELECT METHODS WHERE HasAttribute "NUnit.Framework.SetUpAttribute" AND NbLinesOfCode&#160; > 10_

**Deep inheritance trees in test fixtures**

Again, common test code moved up to a base class and the base class is used in many tests. Then more base classes are created. This creates more tight coupling between test classes. Which makes tests harder to change. Low coupling and high cohesion applies to test code as well. Make each unit test class as independent as possible.

_SELECT TYPES WHERE HasAttribute "NUnit.Framework.TestFixtureAttribute"&#160; AND DepthOfInheritance >2_

**Test fixture setup**

TestFixtureSetup is bad. The <a href="http://www.nunit.org/index.php?p=fixtureSetup&r=2.2.10" target="_blank">TestFixtureSetup</a> is run once before all tests. This leads to fragile tests and inadvertently leads to using some shared state. Use Setup instead

_SELECT METHODS WHERE HasAttribute "NUnit.Framework.TestFixtureSetUpAttribute"_ 

**Tests that fail when they are run in a different order**

The <a href="http://xunit.codeplex.com/wikipage?title=Comparisons&referringTitle=Home" target="_blank">xUnit</a> test runner helps with this, by randomizing the order tests are run.

**Ignored tests**

Ignored tests are like comments. Dead code that doesn’t do anything. Either fix them or delete them.

I have yet to find some way of detecting duplicated tests, shared state in tests and multiple asserts in tests. What other ways can I find test smells ?