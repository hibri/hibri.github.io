---
id: 413
title: Using System.Net Tracing
date: 2005-10-01T23:35:49+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2005/10/01/UsingSystemNetTracing.aspx
permalink: /2005/10/01/using-system-net-tracing/
categories:
  - .Net Net
---
Niftty feature in 2.0,

this is via <http://blogs.msdn.com/dgorti/>

_In Whidbey (.NET Framework 2.0) System.Net has a new feature called
  
Tracing.   
This uses the builtin CLR Tracing functionality. What is
  
interesting about the System.Net Tracing is that  
You can easily&nbsp; see the
  
data that is being sent or received without having to use the NETMON. </p> 

If
  
you have used Network Monitor tools like NETMON/Ethereal you will find that
  
  
there is so much noise that you need to weed through. This can be partially
  
addressed through   
capture filters and display filters. But then looking at a
  
frame in the capture you can&#8217;t  
easily determine which process issued that
  
request. Similarly if there are multiple threads,   
you can&#8217;t easily determine
  
which thread issued that request. One more thing is that if the   
client and
  
server are on the same machine you can;t capture the loop back traffic. Perhaps
  
the most limiting of all   
is that if the application is using SSL (https or
  
FTP with SSL) then it is not possible to look at the traffic.   
You can at
  
most see the TCP frames with encrypted payload. Not much of use.
  
Right?

With System.Net, we addressed all these issues. System.Net tracing
  
is   
1) Per process  
2) Shows threads   
3) Works for SSL   
4) Works for
  
Loopback.  
5) You don&#8217;t need to recompile the code</em>

[Continued..](http://blogs.msdn.com/dgorti/archive/2005/09/18/471003.aspx)