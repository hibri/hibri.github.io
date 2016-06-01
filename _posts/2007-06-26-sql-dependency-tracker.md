---
id: 356
title: SQL Dependency Tracker
date: 2007-06-26T09:31:11+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2007/06/26/SQLDependencyTracker.aspx
permalink: /2007/06/26/sql-dependency-tracker/
categories:
  - .Net Data
---
I was playing with Redgate&#8217;s SQL Dependency tracker yesterday. The balloon tree view sort of shows how modular the db design is. I&#8217;m working on a project where I&#8217;m implementing &#8220;pluggable&#8221; modules of functionality.

The two circular clusters at the top left corner&nbsp;are the db objects for the module I&#8217;m working on. The view shows how the cluster relates to the ASP .Net membership provider tables. The clusters which go diagonally across the view are the aspnet db objects.

<a href="http://www.hibri.net/content/binary/WindowsLiveWriter/SQLDependencyTracker_93E5/image_1.png" atomicselection="true"><img style="border-right: 0px; border-top: 0px; border-left: 0px; border-bottom: 0px" height="392" alt="image" src="http://www.hibri.net/content/binary/WindowsLiveWriter/SQLDependencyTracker_93E5/image_thumb_1.png" width="590" border="0" /></a>