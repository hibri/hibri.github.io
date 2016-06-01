---
id: 341
title: COM Exception while loading a Web Application Project
date: 2008-03-01T13:17:44+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2008/03/01/COMExceptionWhileLoadingAWebApplicationProject.aspx
permalink: /2008/03/01/com-exception-while-loading-a-web-application-project/
categories:
  - .Net General
  - .Net Web
---
VS 2008 throws a COM Exception when loading a web application project. This happens when the project was made in VS 2005 and upgraded using the Upgrade Wizard. It loads web application projects made natively without a problem. There is a work around if this happens to you.

Via [http://www.codeattest.com/blogs/martin/2008/01/comexception-loading-solution.html](http://www.codeattest.com/blogs/martin/2008/01/comexception-loading-solution.html "http://www.codeattest.com/blogs/martin/2008/01/comexception-loading-solution.html")

_&#8220;In order to load the Web Application Project you must make sure that the URL that the project is using, is valid and can be resolved. This can happen pretty often since when you download a project from source control for the first time, it is highly unlikely that you will have the web site already set up.&#8221;_

&nbsp;

If this happens to you, the project will not load and will be grayed out in the solution explorer. Right click and edit the project, (or edit the .csproj file in notepad) look for the WebProjectProperties element. Check if the IISUrl child element points to a valid location. The server should exists, and the virtual directory should point to the same location as the web application project.