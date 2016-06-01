---
id: 317
title: Avoid the slow Add Reference dialog box in Visual Studio 2008
date: 2009-11-28T13:31:31+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2009/11/28/AvoidTheSlowAddReferenceDialogBoxInVisualStudio2008.aspx
permalink: /2009/11/28/avoid-the-slow-add-reference-dialog-box-in-visual-studio-2008/
categories:
  - .Net General
  - development
  - TDD
---
&#160;

When you are in the zone, and want to add a reference to Rhino, NUnit or any other common reference, adding it via the Add Reference dialog can be painfully slow. Fortunately VS has a good automation interface, which lets you to write macros.

I wrote a simple macro to add a NUnit reference to the current project. Add this to your Macros project in Visual Studio, map a button or a shortcut key to it. This way you can add those common references pretty quick. 

This is a cleaned up version of the sample here [http://msdn.microsoft.com/en-us/library/vslangproj80.reference3%28VS.80%29.aspx](http://msdn.microsoft.com/en-us/library/vslangproj80.reference3%28VS.80%29.aspx "http://msdn.microsoft.com/en-us/library/vslangproj80.reference3%28VS.80%29.aspx")

&#160;

<div class="csharpcode">
  <pre><span class="lnum">   1:  </span>    <span class="kwrd">Sub</span> AddNUnitReference()</pre>
  
  <pre><span class="lnum">   2:  </span>        AddNewReference(DTE, <span class="str">"C:\Tools\NUnit\nunit.framework.dll"</span>)</pre>
  
  <pre><span class="lnum">   3:  </span>    <span class="kwrd">End</span> <span class="kwrd">Sub</span></pre>
  
  <pre><span class="lnum">   4:  </span>&#160;</pre>
  
  <pre><span class="lnum">   5:  </span>    <span class="kwrd">Sub</span> AddNewReference(<span class="kwrd">ByVal</span> dte <span class="kwrd">As</span> DTE2, <span class="kwrd">ByVal</span> referencePath <span class="kwrd">As</span> <span class="kwrd">String</span>)</pre>
  
  <pre><span class="lnum">   6:  </span>        <span class="kwrd">Dim</span> aProject <span class="kwrd">As</span> Project</pre>
  
  <pre><span class="lnum">   7:  </span>        <span class="kwrd">Dim</span> aVSProject <span class="kwrd">As</span> VSProject</pre>
  
  <pre><span class="lnum">   8:  </span>&#160;</pre>
  
  <pre><span class="lnum">   9:  </span>        aProject = dte.ActiveDocument.ProjectItem.ContainingProject</pre>
  
  <pre><span class="lnum">  10:  </span>&#160;</pre>
  
  <pre><span class="lnum">  11:  </span>        aVSProject = <span class="kwrd">CType</span>(dte.ActiveDocument.ProjectItem.ContainingProject.<span class="kwrd">Object</span>, VSProject)</pre>
  
  <pre><span class="lnum">  12:  </span>        <span class="rem">' Add an Assembly reference and display its type and additional</span></pre>
  
  <pre><span class="lnum">  13:  </span>        <span class="rem">' information.</span></pre>
  
  <pre><span class="lnum">  14:  </span>        <span class="kwrd">Dim</span> newRef <span class="kwrd">As</span> Reference</pre>
  
  <pre><span class="lnum">  15:  </span>        newRef = aVSProject.References.Add(referencePath)</pre>
  
  <pre><span class="lnum">  16:  </span>&#160;</pre>
  
  <pre><span class="lnum">  17:  </span>    <span class="kwrd">End</span> Sub</pre>
</div>