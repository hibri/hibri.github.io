---
id: 410
title: Cache overuse ?
date: 2005-10-31T08:58:47+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2005/10/31/CacheOveruse.aspx
permalink: /2005/10/31/cache-overuse/
categories:
  - .Net Web
  - High Availability
---
When going through the asp.net forums, one thing I&#8217;ve noticed is that there
  
is a lack of understanding among many devs about ASP .Net caching. The majority
  
of the problems are caused&nbsp;when trying to use the Cache as a reliable
  
in-memory storage medium. The Cache object is not meant to do this.

Cache storage is volatile, It can be garbage collected, it can expire, and it
  
is not expected to be synched in a web farm.

So far I&#8217;ve used the Cache to avoid expensive&nbsp;db hits. I use a
  
refactoring approach to storing data in the Cache.

First I write my usual data access and data binding code with,

<pre><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  </span> Datatable userDataTable;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  </span> userDataTable = DataUtils.GetUsers();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  </span> <span style="COLOR: green">//bind and display</span></pre>

<span style="COLOR: green"></span>&nbsp;

Now to cache the user date, I refactor the code to this,

<pre>DataTable userDataTable;
userData = Cache[<span style="COLOR: maroon">"USER_DATA"]</span>;
<span style="COLOR: blue">if</span>(userData == <span style="COLOR: blue">null</span>){
	userDataTable = DataUtils.GetUsers();
	<span style="COLOR: green">//code to refresh cache, insert etc...
</span>	Cache.Insert(<span style="COLOR: maroon">"USER_DATA"</span>,userDataTable);

}

<span style="COLOR: green">//bind and display</span></pre>

<pre><span style="COLOR: green"></span>&nbsp;</pre>

This simple practice ensures
  
that there is always data, and handles a cache miss gracefully. Any thoughts on
  
this ?