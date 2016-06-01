---
id: 329
title: 'Workaround &ndash; Error while installing VS 2008 SP1 and .Net 3.5 SP1'
date: 2008-08-18T21:58:32+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2008/08/18/WorkaroundNdashErrorWhileInstallingVS2008SP1AndNet35SP1.aspx
permalink: /2008/08/18/workaround-error-while-installing-vs-2008-sp1-and-net-3-5-sp1/
categories:
  - .Net General
---
</p> 

&#160;

If you get an error with the message in the install log like;

dotnetfx35.exe failed with 0x80070643 &#8211; Fatal error during installation

It helps to run a manual cleanup of any .Net 3.5 framework installations before trying again. Use the automated cleanup tool [here](http://blogs.msdn.com/astebner/archive/2006/05/30/611355.aspx "Automated cleanup tool to remove the .NET Framework 1.0, 1.1, 2.0, 3.0 and 3.5"). Remove the .Net 3.5 version already installed. You may need to do it twice to do a complete cleanup. Then start the SP 1 setup again.