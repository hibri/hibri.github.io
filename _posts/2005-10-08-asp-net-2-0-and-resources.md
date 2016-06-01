---
id: 412
title: ASP .Net 2.0 and Resources
date: 2005-10-08T20:33:22+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2005/10/08/ASPNet20AndResources.aspx
permalink: /2005/10/08/asp-net-2-0-and-resources/
categories:
  - .Net Web
---
In VS 2003/ASP .Net 1.1&nbsp;, global resource files (.resx files used by the
  
whole application) compile to thier own assemblies like,
  
assemblyname.resources.dll.

In VS 2005/ASP .Net 2.0 these global resources are kept in the
  
App_GlobalResources directory, and do not compile to individual assemblies.
  
Because of this using the ResourceManager constructor to load the resource
  
assembly does not work in ASP .Net 2.0 because a resource assembly does not
  
exist. .Net 2.0 adds these global resources to their own namespace, and does
  
some runtime magic to load the correct resources.

For example in 2.0, if you have a resource file named myresources.resx, the
  
resource manager object is obtained by

<pre><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  1</span> Resources.myresources.ResourceManager</pre>

This applies to ASP .Net web applications only, the ResourceManager works in
  
the&nbsp;old way in class library project and WinForm apps.

read more [here](http://beta.asp.net/QUICKSTARTV20/aspnet/doc/localization/localization.aspx)

I&#8217;m doing all this on the RTM version of VS 2005, and its looking&nbsp;very
  
good 🙂