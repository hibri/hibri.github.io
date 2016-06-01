---
id: 344
title: Office 2007 SP1 and Vista SP1 RC updates fail to install
date: 2007-12-25T22:11:52+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2007/12/25/Office2007SP1AndVistaSP1RCUpdatesFailToInstall.aspx
permalink: /2007/12/25/office-2007-sp1-and-vista-sp1-rc-updates-fail-to-install/
categories:
  - Vista
---
First tried installing Office SP1 through Windows Update a few times but didn&#8217;t work. The update fails for no apparent reason. The event log shows this;

Product: Microsoft Office Enterprise 2007 &#8212; Error 1935.

An error occurred during the installation of assembly component {04E73476-518E-4B6A-8E10-021A00078847}. HRESULT: 0x80131047. assembly interface: IAssemblyCacheItem, function: Commit, assembly name: Microsoft.Office.Interop.PowerPoint,fileVersion=&#8221;12.0.6211.1000&#8243;,

version=&#8221;12.0.0.0000000&#8243;,culture=&#8221;neutral&#8221;,publicKeyToken=&#8221;71E9BCE111E9429C&#8221;

&nbsp;

Googling for this error, gives me this KB article [http://support.microsoft.com/kb/926804](http://support.microsoft.com/kb/926804 "http://support.microsoft.com/kb/926804"), which recommends repairing the .Net framework&nbsp; 2.0 installation. I can&#8217;t find the .Net 2.0 repair option in the control panel on Vista Ultimate, because this is part of the OS.

I&#8217;m thinking the SP needs only .Net 2.0 to install, so I&#8217;m uninstalling .Net 3.5&nbsp; so that there is only 2.0.

Update : This doesn&#8217;t work either. Hoping MS sees the error reports and posts a fix for this.

Vista SP1 RC also fails to install through Windows Update. The service pack downloads, and the laptop reboots. The installation takes 3 stages, and about 75% into the 3rd stage, the installation fails and starts rolling back. There are no adverse effects because a restore point is created. I&#8217;ll wait for the final release and attempt it again. The update takes a very long time though, so be prepared to spend about 2 to 3 hours on this.