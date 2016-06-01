---
id: 335
title: 99% Uptime ? Nah not for us..
date: 2008-07-05T15:09:35+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2008/07/05/99UptimeNahNotForUs.aspx
permalink: /2008/07/05/99-uptime-nah-not-for-us/
categories:
  - .Net Web
  - High Availability
---
When trying to order pizza today, I get this error on the <a title="Pizza hut website crashes" href="http://www.pizzahut.co.uk/" target="_blank">Pizza Hut</a> web site. The site crashed when making my transaction , and I had to call the bank&nbsp; to check if the transaction went through.

[<img style="border-top-width: 0px; border-left-width: 0px; border-bottom-width: 0px; border-right-width: 0px" border="0" alt="pizza-hut-error" src="http://www.hibri.net/content/binary/WindowsLiveWriter/313911e61d04_C78E/pizza-hut-error_thumb.png" width="644" height="391" />](http://www.hibri.net/content/binary/WindowsLiveWriter/313911e61d04_C78E/pizza-hut-error_2.png) 

Is it really that hard to show some care when&nbsp; running a web site ? I mean, it doesn&#8217;t take a lot to turn on&nbsp; <a title="customErrors element" href="http://msdn.microsoft.com/en-us/library/h0hfz6fc.aspx" target="_blank">Custom Error pages on the web.config</a> and turn off <a title="Asp.net web.config debug mode" href="http://blogs.msdn.com/tess/archive/2006/04/13/575364.aspx" target="_blank">debug mode.</a> Having this sort of error shown on a public web site that is getting a lot of traffic shows <a href="http://www.adactus.co.uk/" target="_blank">lack of care, lack of planning and un-professionalism by whoever built and runs this site</a>. Expecting something to fail and handling the failure gracefully shows that the developer has planned for the unexpected. But not in this instance.&nbsp; From this it is likely that the site owners didn&#8217;t use some decent infrastructure to handle fail over, they didn&#8217;t think of what could go wrong. I was still getting this for about an hour means that they don&#8217;t have anyway of getting notified to fix it. 99% uptime ? Nah, not for us. 

Would I trust my credit card details with them again ? Nope..

Maybe it was because they used business <a href="http://www.rackspace.co.uk/default.asp?docId=14682&productGroupId=15884" target="_blank">objects written by Van Halen</a>.