---
id: 480
title: 'Unit testing time eaters: Getting past them'
date: 2011-05-04T20:16:56+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/?p=480
permalink: /2011/05/04/unit-testing-time-eaters-getting-past-them-2/
categories:
  - Agile
  - development
  - TDD
---
I was reading [http://7enn.com/2011/05/02/the-biggest-time-eater-in-unit-testing/](http://7enn.com/2011/05/02/the-biggest-time-eater-in-unit-testing/ "http://7enn.com/2011/05/02/the-biggest-time-eater-in-unit-testing/") the other day. 

How do we get past the discovery phase without getting stuck ? 

My suggestion is to start the tests with what you know and go with it. Think about it as we write the test. It will become clearer gradually. 

I’ll explain with an example.

The test name. This is the part where most of us get stuck. It’s an art. Getting it right is solving half the problem, but lets not get stuck on it. It doesn’t matter if we don’t have the perfect test name at the start. Give it a name that is good enough. 

<pre class="csharpcode">[Test]
<span class="kwrd">public</span> <span class="kwrd">void</span> Foo () {

}</pre>

&nbsp;

This is all we need for now. 

We have name, we have a test, our test runner can run the test.

Next. What is the proper outcome to test for ?.&nbsp; In other words what are we testing ?

Start with the assert first.&nbsp; Assume we want the title property in some object set to the expected value. Don’t worry about what type the object is, if you don’t have it already.

<pre class="csharpcode">[Test]
<span class="kwrd">public</span> <span class="kwrd">void</span> Foo (){

  Assert.That(fooObject.Title, Is.EqualTo(expectedTitle));

}</pre>



Start with the smallest thing you can assert. Let’s not be concerned with all the other things that need to be tested. In the example code above, I’m testing that an object named fooObject has it’s Title property set to the expected string. At this point I’m not concerned about the exact value of the expectation.

We have an assert. Something needs to happen in the thing we are testing. This is the action. Think about where we get fooObject from.

Some action needs to be executed to get an instance. This action is a method. In code , the way to make something happen is to call a method.

Create a method. Let’s not get stuck on the name too much. I’ll call it Get(). Calling Get() gives me fooObject.

<pre class="csharpcode">[Test]
<span class="kwrd">public</span> <span class="kwrd">void</span> Foo (){

   var fooObject = controller.Get();  
  Assert.That(fooObject.Title, Is.EqualTo(expectedTitle));

}</pre>

&nbsp;

We have an assert and an action. The code even compiling yet. Keep typing.

Our object controller needs to be an instance of something. Is this an existing object we are testing ?, if not I’ll create it.&nbsp; We always have a context in which we are writing a unit test. This gives us an indication on what the thing we are testing should be called. 

In this example, we are testing a Controller. Instantiate the controller object.

<pre class="csharpcode">[Test]
<span class="kwrd">public</span> <span class="kwrd">void</span> Foo (){

 var controller = <span class="kwrd">new</span> HomeController();

  var fooObject = controller.Get();  
 
 Assert.That(fooObject.Title, Is.EqualTo(expectedTitle));

}</pre>



Next use resharper ( or similar tool for your language) to create the missing objects. Let’s make the code compile at this time. Give a value for the expectation. Don’t worry about which project (in Visual Studio) the classes will be in. It’s fine to keep it in the test class for now.

<pre class="csharpcode">[Test]
<span class="kwrd">public</span> <span class="kwrd">void</span> Foo (){

<span class="kwrd">string</span> expectedTitle = <span class="str">"some title"</span>;
 var controller = <span class="kwrd">new</span> HomeController();

  var fooObject = controller.Get();  
 
 Assert.That(fooObject.Title, Is.EqualTo(expectedTitle));

}</pre>

<pre class="csharpcode">&nbsp;</pre>

We have an assert, action and arrange. Read it the other way.&nbsp; Arrange, Act and Assert. The 3 parts we need for a test.

Run the test, see it fail. Write the bare minimum of code to make the test pass. Even hardcode things. Get a green bar. Even give temporary names. 

Let’s refactor.&nbsp; Rename things. The test is much more clearer now. Rename Foo to ShouldSetTitleOnView.&nbsp; 

Run the tests again, and keep renaming things. Move files to where they should be.

At this point we can think about injecting dependencies. Remember those hard coded values we put in to make the test pass ? 

Inject a dependency to give those values. There is now a place to inject dependencies, the constructor of the HomeController. 

To summarize,

Writing the assert first, gives a focal point for the test. Working backwards from this focal point ensures that we write the bare minimum code needed to make the test pass. We don’t need to worry about injecting dependencies that are not even relevant to what we are asserting.

Avoid thinking about your team/company standards of how you should write your tests. Just write the test with what you know. You can always rename things later when you have a green bar to the appropriate standard.

You can follow the same pattern even in unit tests, integration tests or acceptance tests. By doing this we speed up our discovery phase by writing the tests. 

&nbsp;

&nbsp;

&nbsp;

&nbsp;