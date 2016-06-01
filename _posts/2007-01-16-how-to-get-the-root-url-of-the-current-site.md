---
id: 369
title: How to get the root url of the current site
date: 2007-01-16T11:17:33+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2007/01/16/HowToGetTheRootUrlOfTheCurrentSite.aspx
permalink: /2007/01/16/how-to-get-the-root-url-of-the-current-site/
categories:
  - .Net Web
---
I have situations where I need the domain name and the application path of the current page (request ).

if the current request was **http://www.myserver.com/website1/page.aspx**

I need **http://www.myserver.com/website1**. Though the web.config can store this setting, I don&#8217;t want to change the config each time I move the site between servers.

So here is a little function I wrote.

Request.Url.AbsoluteUri&nbsp;&nbsp; gives **http://www.myserver.com/website1/page.aspx**

Request.ApplicationPath gives /website1/. Subtract page.aspx from http://www.myserver.com/website1/page.aspx

&nbsp;

<span style="color: blue">public</span> <span style="color: blue">static</span> <span style="color: blue">string</span> GetSiteUrl() {

> if (HttpContext.Current.Request.ApplicationPath == &#8220;/&#8221;) {  
> &nbsp;&nbsp;&nbsp;&nbsp; return &#8220;/&#8221;  
> }

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;<span style="color: blue">string</span> url = HttpContext.Current.Request.Url.AbsoluteUri;  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <span style="color: blue">int</span> end = url.IndexOf(HttpContext.Current.Request.ApplicationPath) +   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; HttpContext.Current.Request.ApplicationPath.Length;  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url = url.Substring(<span style="color: maroon"></span>, end);  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <span style="color: blue">return</span> url;  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }

<pre>&nbsp;</pre>