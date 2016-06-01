---
id: 404
title: Timers and synchronization
date: 2005-12-28T22:36:32+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2005/12/28/TimersAndSynchronization.aspx
permalink: /2005/12/28/timers-and-synchronization/
categories:
  - .Net Data
  - .Net UI
---
While working with the System.Timers.Timer class last week, I found that the
  
timer_elapsed method is not synchronized, i.e the event is fired without waiting
  
for the completion of the previous invocation.

Say for example you have a method that pulls up the latest records from a
  
table and do some processing. The timer event can fire while you are doing this
  
processing and have still not marked the records as processed. The safe way is
  
to wrap the code in the timer_elapsed event inside a lock
  
statement.