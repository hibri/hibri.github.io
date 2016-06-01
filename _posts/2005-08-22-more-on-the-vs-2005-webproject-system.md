---
id: 420
title: More on the VS 2005 Webproject system.
date: 2005-08-22T09:55:29+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2005/08/22/MoreOnTheVS2005WebprojectSystem.aspx
permalink: /2005/08/22/more-on-the-vs-2005-webproject-system/
categories:
  - .Net Web
---
A [A](http://weblogs.asp.net/scottgu/archive/2005/08/21/423201.aspx) by Scott Guthrie. The features
  
are interesting, but not implemented in Beta 2 or are buggy. MS expects all of
  
this to be in the final release.

To summarise,

No need for Frontpage server extensions on the server or development machine.
  
Just install VS 2005 and you are good to go. No need for IIS too. This is good
  
cos now it would be possible to test web apps using Apache and the mod_dotnet
  
module.

There is no web project file. The project infers the contents from the file
  
system.&nbsp;With this there would be no more mapping a IIS virtual directory
  
for a web project. Very useful when you want someone else to open your web
  
project.

There is a &#8220;hit refresh to compile&#8221; feature. Say you make a change to a page
  
or a code behind file, now just refresh the page for it to compile.

Anyways thats just a lil bit of what interests me. The has been quite a bit
  
of confusion regarding the new web project system, and this post clears some of
  
that. However, I&#8217;ll have to wait and see how this all works in the Final
  
version.

&nbsp;