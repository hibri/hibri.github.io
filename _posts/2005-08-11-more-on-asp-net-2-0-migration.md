---
id: 424
title: More on ASP .Net 2.0 migration..
date: 2005-08-11T19:42:38+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2005/08/11/MoreOnASPNet20Migration.aspx
permalink: /2005/08/11/more-on-asp-net-2-0-migration/
categories:
  - .Net Web
---
As posted earlier I&#8217;m trying to migrate Dasblog from 1.1 to 2.0. Visual
  
studio refused to compile aspx pages in the dasblog webproject after the
  
conversion. The aspx pages did not see the custom controls the custom controls
  
that were used by the pages and the compiler was throwing missing reference
  
errrors. The controls themselves did not have any errors and compiled
  
individually but will not show up in Intellisense and the class viewer. None of
  
the pages showed up in the class viewer. I even tried adding a new page, but
  
still no luck.

Googling for this got me here <http://west-wind.com/weblog/posts/2130.aspx>.
  
Well atleast I&#8217;m not alone in this. The reason for this seems to be partial
  
classes. Now partial classes are combined to a complete class at compile time
  
and for some reason these complete classes made of partial classes are not
  
visible at design time. I&#8217;m using the February 2005 CTP release of Visual Studio
  
2005. I dont have a solution yet..so I&#8217;ve paused this conversion project for
  
now. I&#8217;ll try it again when I get the June 2005 release or the final. 

If any of you have had this problem and solved it please let me
  
know&#8230;