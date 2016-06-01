---
id: 320
title: Continuous TDD with Autobuild .Net
date: 2009-08-27T13:53:40+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2009/08/27/ContinuousTDDWithAutobuildNet.aspx
permalink: /2009/08/27/continuous-tdd-with-autobuild-net/
categories:
  - Agile
  - TDD
---
I like the idea of running unit tests continuously as I type and save code.&#160; I read

<div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:742324d9-c55a-49e3-ad59-bf71b7bfba50" class="wlWriterEditableSmartContent">
  Technorati Tags: <a href="http://technorati.com/tags/TDD" rel="tag">TDD</a>
</div>

about [Autobuild .Net](http://timross.wordpress.com/2009/08/04/continuous-testing-in-net/) recently. This is easy to setup and use.

Grab the&#160; code from [http://code.google.com/p/autobuildtool/](http://code.google.com/p/autobuildtool/ "http://code.google.com/p/autobuildtool/")&#160; build it by running the default.build script.

When this is built successfully, the build process creates the tool in the output directory.

Copy the contents of this output directory to the project where you want autobuild to work on.

Autobuild .Net runs a nant build script each time a file is saved in a specific path being watched.

Change the autobuild.build script with the path to the solution file and the path to the unit test assembly.

Next in autobuild.cmd , change the first argument to the directory to watch for changes. The second argument is for the path to autobuild.build. This is the nant build script that autobuild will execute. You can replace this with an existing Nant build script.

Run atuobuild.cmd . That&#8217;s it. Type some code, save it and watch the window go red because it didn’t compile. Make it compile and watch it go green.

Write a failing test and see it go red, make it pass and see it go green. Fun eh ? 🙂