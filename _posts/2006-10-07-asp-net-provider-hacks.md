---
id: 378
title: ASP .Net Provider Hacks
date: 2006-10-07T20:46:03+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2006/10/07/ASPNetProviderHacks.aspx
permalink: /2006/10/07/asp-net-provider-hacks/
categories:
  - .Net Web
---
&nbsp;

A few issues to keep in mind when converting a VS 2005 web project to a Web Application project.

[http://webproject.scottgu.com/CSharp/Migration2/Mi&#8230;](http://webproject.scottgu.com/CSharp/Migration2/Migration2.aspx)

ASP .Net automatically generates a strongly typed Profile class when using Profile Personalization (System.Web.Profiles). This does not happen when using WAP (Web application projects).

There is a free utility to generate the Profile class from the web.config

[http://www.gotdotnet.com/workspaces/workspace.aspx&#8230;](http://www.gotdotnet.com/workspaces/workspace.aspx?id=406eefba-2dd9-4d80-a48c-b4f135df4127)

The default SqlProfilesProvider works by serializing all the profile properties into one column. However, as with all providers this can be changed. 

[http://www.asp.net/downloads/teamprojects/default&#8230;.](http://www.asp.net/downloads/teamprojects/default.aspx?tabid=62#tableprofile)&nbsp;is a download to a Table profile provider and stored procedure profile provider. These work out of the box, to a profiles table of your own choosing.