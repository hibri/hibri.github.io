---
id: 319
title: When all fails, extract method
date: 2009-08-30T10:18:18+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2009/08/30/WhenAllFailsExtractMethod.aspx
permalink: /2009/08/30/when-all-fails-extract-method/
categories:
  - Uncategorized
---
Sometimes (most of the time) when looking at a piece of un-clean code, it’s not clear what path to take to make the code that little bit more better. The easiest first refactoring to do is <a href="http://www.refactoring.com/catalog/extractMethod.html" target="_blank">extract method</a>.&#160; Use extract method ruthlessly. Attempt to get and get many smallest methods. Repeat till these methods become smaller and smaller as close as possible to one line of code in a method.

Patterns emerge when creating more and more methods. The methods start to show groupings and responsibilities. When the methods obey the <a href="http://www.c2.com/cgi/wiki?LawOfDemeter" target="_blank">Law of Demeter</a>, they can be moved around to other classes and also create new classes. It becomes easier to see duplication.

Methods are the smallest building blocks of a piece of software. These small and granular building blocks are more flexible. They give more ways to build things and allow greater reuse. When these building blocks are available, the code becomes much clearer. The big refactorings are made possible.