---
id: 454
title: Optimize memory for Windows
date: 2005-03-26T18:10:16+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2005/03/26/OptimizeMemoryForWindows.aspx
permalink: /2005/03/26/optimize-memory-for-windows/
categories:
  - Windows
---
[<FONT face=Verdana>http://www.rojakpot.com/default.aspx?location=3&var1=143&var2=0</FONT>](blocked::http://www.rojakpot.com/default.aspx?location=3&var1=143&var2=0)


  


<FONT face=Verdana>A very helpful article to optimize your Windows system. I&#8217;ve tried the suggestions on my Windows XP Pro laptop. There is a significant and noticeable difference now. Diskeeper is required to defragment the hard drive and the page file. A </FONT>[<FONT face=Verdana>trial version </FONT>](blocked::http://consumer.execsoft.com/downloads/downloads.asp?RID=50&SId=2&CId=1)<FONT face=Verdana>of Diskeeper is available.</FONT>


  


<FONT face=Verdana>The article provides a good explanation of Windows memory fundamentals. A free page file defragmentation utility is available from </FONT>[<FONT face=Verdana>Sysinternals</FONT>](blocked::http://www.sysinternals.com/ntw2k/freeware/pagedefrag.shtml)<FONT face=Verdana>.</FONT>


  


<FONT face=Verdana>This is what I have done to my system (Intel Centrino 1.6 GHz, 512 MB RAM, 60GB).</FONT>


  



  


  1. <FONT face=Verdana>Install Diskeeper, and defragment the hard disc.</FONT>
  
      * <FONT face=Verdana>Check the page file usage using the taskmanager performance tab. Monitor the max size under normal use(Outlook, winamp, OneNote,Word, Visual Studio,Opera,Azureaus).</FONT>
  
          * <FONT face=Verdana>In the virtual memory settings, set the initial size to 512 MB and the maximum size to 768MB.<SPAN class=511130618-26032005>&nbsp;</SPAN></FONT>
  
              * <FONT face=Verdana>Use Diskeeper to defragment the page file at the next boot.</FONT>
  
                  * <FONT face=Verdana>Schedule Diskeeper to run regularly.</FONT></OL></p>