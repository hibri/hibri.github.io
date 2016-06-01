---
id: 362
title: New features in IIS 7.0
date: 2007-04-03T09:15:55+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2007/04/03/NewFeaturesInIIS70.aspx
permalink: /2007/04/03/new-features-in-iis-7-0/
categories:
  - .Net Web
---
[Scott blogs about the new features in IIS 7.0](http://weblogs.asp.net/scottgu/archive/2007/04/02/iis-7-0.aspx) server version coming out later this year. One set of features that I think is really really amazing :

_&#8220;The web farm support in particular is really cool, and will allow you to deploy your web applications on a file-share that contains all of the code, configuration, content, and encryption keys needed to run a server.&nbsp; You can then&nbsp;add any number of stateless and configuration-less web-servers into a web farm and just point them at the file-server to dynamically load their configuration settings (including bindings, virtual directories, app pool settings, etc) and application content.&nbsp; This makes it trivial to scale out applications across machines, and avoid having to use replication schemes for&nbsp;configuration and application deployment (just copy over the files on the file-share and all of the machines in the web farm will immediately pick up the changes).&nbsp;&#8220;_

I already use source control to deploy files to the web farm so replication is not a big issue, but it is a pain to configure sites for the first time on each server.

[More on this](http://msdn.microsoft.com/msdnmag/issues/07/03/IIS7/)