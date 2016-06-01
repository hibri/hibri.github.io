---
id: 399
title: URL Rewriting for ASP .Net
date: 2006-02-05T18:38:02+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2006/02/05/URLRewritingForASPNet.aspx
permalink: /2006/02/05/url-rewriting-for-asp-net/
categories:
  - .Net Web
---
&nbsp;<http://www.urlrewriting.net/>
  
has a free URL re-writing HTTP module for ASP .Net with source code. This
  
supports regular expressions. This is a must have for every ASP .Net developer.
  
I haven&#8217;t compared this to the Apache mod_rewrite module yet, which I would say
  
is very powerful. 

My view is that URL rewriting is best implemented in the web server (IIS),
  
just like the implementation in Apache. This would give URL rewriting
  
functionality regardless of the file type served. I have yet to see a (free ?
  
)&nbsp;URL rewriting module for IIS, that gives all the features of Apache
  
mod_rewrite.

Will we see this in IIS 7 ?