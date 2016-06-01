---
id: 390
title: 'HOWTO : Set a FTP home directory using IIS'
date: 2006-06-02T15:45:18+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2006/06/02/HOWTOSetAFTPHomeDirectoryUsingIIS.aspx
permalink: /2006/06/02/howto-set-a-ftp-home-directory-using-iis/
categories:
  - .Net Web
  - Windows
---
If&nbsp; you want a&nbsp;FTP login to change to a directory upon login heres
  
what to do.

Create a vritual directory or directory with the same name as the user
  
login

If the user login is john, create a directory under the FTP root named
  
&#8220;john&#8221;. On logging in john will access <ftp:///ftp.myserver.com/john>.

&nbsp;

&nbsp;