---
id: 371
title: Sitefinity
date: 2007-01-13T20:23:51+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2007/01/13/Sitefinity.aspx
permalink: /2007/01/13/sitefinity/
categories:
  - .Net Web
---
During the past couple of weeks I&#8217;ve been evaluating content management systems. My core requirements were; 

1. Built with C#, .Net 2.0 

2. Modular structure like SharePoint. 

3. Granular permissions. Page and section level. 

4. CSS and XHTML support. 

I started building one from scratch; I wanted the CMS to leverage all the features of ASP .Net 2.0, such as master pages, membership and themes. The open source solutions didn’t impress me much. Dotnetnuke did not have a lot of flexibility (for me). I didn’t spend too much time with DNN because it was written in VB .Net. 

While I was building my CMS, I found [Sitefinity](http://www.sitefinity.com) built by [Telerik](http://ww.telerik.com). Sitefinity is a pure .Net 2.0 solution. Written in C# and a killer feature is that it comes with the Telerik rad controls. The upcoming 3.0 version uses master pages for layout. The CMS engine detects the placeholder controls and uses them as containers for CMS driven content. 

Extending Sitefinity is as easy as opening the generated website in Visual Studio as a web project. The experience is analogous to a situation where someone had already written the core CMS and given the project to extend. Sitefinity host simple ASP .Net controls. So developing a solution is the same as any other ASP .Net project. This is a big advantage for me, as I don’t have to go and learn a new framework. Sitefinity uses the native ASP .Net provider model. This makes Sitefinity come close to SharePoint 2007. This all applies to v3.0; the previous version 2.7 does not use master pages and recursive table layout model, which did not support CSS layouts. Version 3.0 is in beta, with the final release in February. 

So if you are developing content management systems, Sitefinity definitely should be on top of your list. 

PS : This is not a free solution, but well worth the money&nbsp;it in my opinion. Telerik should be banging the drum on this one :).

PPS : I don&#8217;t work for Telerik, though my company has purchased an enterprise licence.