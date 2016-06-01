---
id: 372
title: CSS Adapter for the SiteMapPath control.
date: 2006-12-03T11:42:43+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2006/12/03/CSSAdapterForTheSiteMapPathControl.aspx
permalink: /2006/12/03/css-adapter-for-the-sitemappath-control/
categories:
  - .Net Web
---
Wrote a [CSS Adapter](http://www.asp.net/cssadapters/) for the SiteMapPath control. I wanted a breadcrumb trail with clean link tags only. Renders a clean set of link tags within a div tag (and optionally a span tag). 

Usage:

Add the [SiteMapPathAdapter.cs](http://www.hibri.net/content/binary/SiteMapPathAdapter.txt) file to your web project. (rename the .txt file to .cs)

Add a .browser file to the web site. Add the following entry in the controlAdapters element.

<pre><span style="color: blue">&lt;</span><span style="color: maroon">adapter</span> <span style="color: red">controlType </span>="<span style="color: blue">System.Web.UI.WebControls.SiteMapPath</span>"
               <span style="color: red">adapterType </span>="<span style="color: blue">SiteMapPathAdapter</span>" /<span style="color: blue">&gt;</span></pre>

&nbsp;

Drag and drop the control on to the web form

<span style="color: blue"><</span><span style="color: maroon">asp:SiteMapPath</span> <span style="color: red">ID</span>=&#8221;<span style="color: blue">SiteMapPath1</span>&#8221; <span style="color: red">runat</span>=&#8221;<span style="color: blue">server</span>&#8221; <span style="color: red">CssSelectorId</span>=&#8221;<span style="color: blue">breadcrumbs</span>&#8221; <span style="color: blue">></span>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <span style="color: blue"><</span>/<span style="color: maroon">asp:SiteMapPath</span><span style="color: blue">></span> 

Use the CssSelectorId attribute to give the surrounding div an identifier.

More on CSS Adapters

<a title="CSS Control Adapter Toolkit for ASP.NET 2.0" href="http://weblogs.asp.net/scottgu/archive/2006/05/02/CSS-Control-Adapter-Toolkit-for-ASP.NET-2.0-.aspx" target="_blank">CSS Control Adapter Toolkit for ASP.NET 2.0</a>

[Architectural Overview of Adaptive Control Behavior](http://msdn2.microsoft.com/en-us/library/67276kc5.aspx "Architectural Overview of Adaptive Control Behavior")

[Browser Definition file schema](http://msdn2.microsoft.com/en-us/library/ms228122.aspx)