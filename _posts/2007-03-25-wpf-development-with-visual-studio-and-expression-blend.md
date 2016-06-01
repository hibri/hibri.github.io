---
id: 364
title: WPF development with Visual Studio and Expression Blend
date: 2007-03-25T21:34:32+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2007/03/25/WPFDevelopmentWithVisualStudioAndExpressionBlend.aspx
permalink: /2007/03/25/wpf-development-with-visual-studio-and-expression-blend/
categories:
  - Uncategorized
---
Started work on a small personal project using WPF and ClickOnce today. I&#8217;m using Expression Blend (RC) to design the interface and VS for the code. I can open the same VS project in Expression Blend, both environments detect file changes but with that popup message. Blend makes it easier to add controls and set properties, but it lacks intellisense, tag completion and code formatting that the VS XAML editor has. I hope this is added in the final version. 

Here are a few reasons why I think WPF/E is better than Flash, though I think it won&#8217;t be a Flash killer yet. 

  1. Data binding: Flash does not come with any of this out of the box, it has to be done using Action script. WPF has extensive support for data binding. Binding to an XML data source is done easily in XAML using declarative code. This makes it easier for the designer types to add data integration without having to rely on an action script developer for the task.   
    Update : WPF/E however does not have databinding in the current CTP build. See point 3, which makes it not so bad. 
      * Source is available: If I find really cool whizz bang work created with WPF, I can look at the source and see how it&#8217;s done. This is similar to HTML and CSS where one can look at the code and copy/learn/link. This leads to more reusable code and gets people sharing great WPF implementations. Can&#8217;t do this with Flash now, unless a decompiler is used. 
          * Generate XAML from the server: Since all it takes is to have the web server serve up a xml file it is possible to generate customized interfaces based on backend data. <a href="http://weblogs.asp.net/plip/archive/2006/04/29/444457.aspx" target="_blank">XAML from ASP .Net</a> </ol> 
        More on WPF vs. Flash 
        
        [http://donburnett.wordpress.com/2007/03/07/poor-maligned-and-misunderstood-by-many-wpfe/](http://donburnett.wordpress.com/2007/03/07/poor-maligned-and-misunderstood-by-many-wpfe/ "http://donburnett.wordpress.com/2007/03/07/poor-maligned-and-misunderstood-by-many-wpfe/")
        
        <http://thewpfblog.com/?p=17> 
        
        <http://www.nukeation.net/PermaLink,guid,ea198313-623e-400f-be22-82c242b5812c.aspx>