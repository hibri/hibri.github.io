---
id: 504
title: Mocking HTTP Servers
date: 2011-06-11T13:03:44+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/?p=504
permalink: /2011/06/11/mocking-http-servers/
categories:
  - API
  - development
  - TDD
  - Uncategorized
tags:
  - "acceptance tests"
  - http
  - mocking
  - tests
---
### The problem

There are tests (mostly what we call acceptance tests). The system under test (SUT) works with a couple of web services to do its work. The problem I&#8217;m faced with is that, when I write these tests, the external web services have to be arranged with data for the test, or the test has to rely on existing data. Writing these tests is extremely painful. Knowledge of the magic existing data is required and in the end what we are really writing are integration tests. But we don&#8217;t want integration tests.

At [7digital](http://blogs.7digital.com/dev/), we are exposing more of our domain via HTTP APIs, in a “NotSOA” manner. To test each service by itself it becomes necessary to mock the dependencies.

### Solutions.

There are a couple of solutions to this.
  
Set up an stub HTTP web service somewhere, and let it return canned responses. It behaves like the real web service, but only returns responses that have been arranged. The disadvantage of this approach is that I have to know about what canned responses have already been setup.

To change the response for a particular test I have to make changes to the stub server and deploy it, as it is a separate application. It takes the focus away from writing the test I&#8217;m concerned with.

Another way is to insert some sort of &#8220;switch&#8221; in production code that will return canned responses when under test. I don&#8217;t like this approach because it requires production code just for tests

### My solution.

What I want to do is something similar to setting up mocks/stubs in unit tests, but to do it with an actual http server. To setup the stubbed responses in the test code itself, and not to have to make any change to production code, other than a configuration change.

So this is what I came up with

<div class="csharpcode">
  <pre class="alt"><span class="lnum"> 1: </span>[Test]</pre>
  
  <pre><span class="lnum"> 2: </span>        <span class="kwrd">public</span> <span class="kwrd">void</span> SUT_should_return_stubbed_response() {</pre>
  
  <pre class="alt"><span class="lnum"> 3: </span>            IStubHttp stubHttp = HttpMockRepository</pre>
  
  <pre><span class="lnum"> 4: </span>                .At(<span class="str">"http://localhost:8080/someapp"</span>);</pre>
  
  <pre class="alt"><span class="lnum"> 5: </span></pre>
  
  <pre><span class="lnum"> 6: </span></pre>
  
  <pre class="alt"><span class="lnum"> 7: </span>            <span class="kwrd">const</span> <span class="kwrd">string</span> expected = <span class="str">"&lt;xml&gt;&lt;&gt;response&gt;Hello World&lt;/response&gt;&lt;/xml&gt;"</span>;</pre>
  
  <pre><span class="lnum"> 8: </span>            stubHttp.Stub(x =&gt; x.Get(<span class="str">"/someendpoint"</span>))</pre>
  
  <pre class="alt"><span class="lnum"> 9: </span>                .Return(expected)</pre>
  
  <pre><span class="lnum"> 10: </span>                .OK();</pre>
  
  <pre class="alt"><span class="lnum"> 11: </span></pre>
  
  <pre><span class="lnum"> 12: </span>            <span class="kwrd">string</span> result = <span class="kwrd">new</span> SystemUnderTest().GetData();</pre>
  
  <pre class="alt"><span class="lnum"> 13: </span></pre>
  
  <pre><span class="lnum"> 14: </span>            Assert.That(result, Is.EqualTo(expected));</pre>
  
  <pre class="alt"><span class="lnum"> 15: </span></pre>
  
  <pre><span class="lnum"> 16: </span>        }</pre>
</div>

<!-- .csharpcode, .csharpcode pre { 	font-size: small; 	color: black; 	font-family: consolas, "Courier New", courier, monospace; 	background-color: #ffffff; 	/*white-space: pre;*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt  { 	background-color: #f4f4f4; 	width: 100%; 	margin: 0em; } .csharpcode .lnum { color: #606060; } -->

HttpMockRepoisitory.At creates a HTTP server listening on port 8080, and behaves as if it is process request under the /someapp path. This is the web service that the SUT will get it’s data from.

Using the object returned,  it is possible to setup stubbed responses using a fluent syntax. The stub server can return text and files. I’ve posted a few more examples on github [http://github.com/hibri/HttpMock/blob/master/src/HttpMock.Integration.Tests/HttpEndPointTests.cs](http://github.com/hibri/HttpMock/blob/master/src/HttpMock.Integration.Tests/HttpEndPointTests.cs "https://github.com/hibri/HttpMock/blob/master/src/HttpMock.Integration.Tests/HttpEndPointTests.cs")

&nbsp;

### Kayak.

I’m using <a href="http://kayakhttp.com/" target="_blank">Kayak</a>, a light weight, asynchronous HTTP server written in C#. Kayak, can accept request processing delegates, and post them to the HTTP server listening on the given socket. This allows me to add stub responses at runtime.

### Current status.

This is very much a work in progress. HTTP GET works. There is support for returning stubbing content types and HTTP return codes. I’ll be able to add to this while changing a very large test suite to not rely on real web services.  I’ve created a repository on github at [http://github.com/hibri/HttpMock](http://github.com/hibri/HttpMock "https://github.com/hibri/HttpMock")

There are no unit tests now, but I’ll be adding them soon as I wanted to prove the concept first.

Describing this as mocking is not entirely correct, but I couldn’t find a term to describe the concept. It is possible to do the same in Ruby using Sinatra.