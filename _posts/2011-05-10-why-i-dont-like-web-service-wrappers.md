---
id: 487
title: 'Why I don&rsquo;t like web service wrappers'
date: 2011-05-10T20:32:44+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2011/05/10/why-i-dont-like-web-service-wrappers/
permalink: /2011/05/10/why-i-dont-like-web-service-wrappers/
categories:
  - API
tags:
  - API
---
Martin Fowler’s post [http://martinfowler.com/bliki/TolerantReader.html](http://martinfowler.com/bliki/TolerantReader.html "http://martinfowler.com/bliki/TolerantReader.html") mirrors my thoughts on consuming web services. 

### What is a web service wrapper ?

A wrapper for a web service is a library, helps you deal with said service in the language programming language of your choice. It hides the details of the web service, and saves you the trouble of having to know how to parse XML or JSON. The wrapper gives you first class objects to work with.

Many web service providers provide a wrapper for their services in most programming languages.

### Why I don’t like wrappers.

I strongly believe that web services should be simple to use. If you expose a web service via HTTP, your consumers should be able to use any HTTP client to consume the service.

You should be able to use a web service by simply typing the URL for the web service method in the web browser’s address bar and see the result in the browser itself.&#160; You should be able to use a command line tool such as <a href="http://curl.haxx.se/" target="_blank">curl</a> to call the web service. Using a web service should not be more complicated than this. If you were hardcore even telnet should suffice.

To consume the service in code, the bare minimum a&#160; developer should need is a decent HTTP client library and a standard XML/JSON parser. Even a decent string library should suffice to make sense of the HTTP responses. These are pretty much available in the framework provided out of the box with the major programming languages. Of course there are situations where you’ll need more, but then this should be the exception and not the norm.

From the point of view of a web service provider, this simplicity increases adoption of your web service. Consumers don’t have to wait for you publish a new version of the wrapper library in order to start using a new service endpoint. Maintenance of the wrapper library is a non-issue, as you can focus on fixing issues with the service only, and not the wrapper library.

### Avoid using wrappers internally.

When building a web service, avoid the temptation to use wrappers in your acceptance and integration tests. Strongly typed wrappers are a bad idea. I’ve seen this first hand when writing tests when building the <a href="http://developer.7digital.net/" target="_blank">7digital API</a>. Don’t even parse responses to strongly typed objects. I’ve forbidden the use of wrappers and strongly typed objects for testing the 7Digital API within my team.

The reason for this is, as a provider, you have to use the service as a consumer would. Wrappers hide the complexity of your own service, and you won’t know how complex the service has become.&#160; When you work with bare HTTP response strings, you will see potential usability issues that consumers will face.

### Publish sample code, but not wrappers.

If you are providing a web service, my recommendation is to publish sample code, and not wrappers around your service. Show developers how to consume the service in their favorite programming languages. A good idea is to give them tests as Martin Fowler recommends. The tests can serve as sample code. They can run those tests against your service and see where the problem lies.

### Thoughts

In my experience, using a strongly typed language such as C# has been a bad idea.&#160; Dynamic languages like Ruby can be used to write more tolerant wrappers. This is because with Ruby you can evaluate the API responses at run time rather than having to use an object that requires the response to be in a certain format.