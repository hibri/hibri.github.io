---
id: 408
title: Use VS 2005 Beta2 to target .NET Runtime 1.1
date: 2005-11-10T18:17:06+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2005/11/10/UseVS2005Beta2ToTargetNETRuntime11.aspx
permalink: /2005/11/10/use-vs-2005-beta2-to-target-net-runtime-1-1/
categories:
  - Uncategorized
---
<p dir="ltr">
  <span><span>Via <a href="http://blogs.msdn.com/jomo_fisher/archive/2005/04/22/410903.aspx">http://blogs.msdn.com/jomo_fisher/archive/2005/04/22/410903.aspx</a></span></span>
</p>

<blockquote class="Section1" dir="ltr">
  <p>
    <span></p> 
    
    <p>
      <em><span><span>(1)<span>&nbsp;&nbsp; </span></span></span><span>Copy <a href="http://blogs.msdn.com/jomo_fisher/articles/410896.aspx">this</a> <span class="SpellE">MSBuild</span> targets file to “C:\program files\<span class="SpellE">msbuild\CrossCompile.CSharp.targets</span>”<?xml:namespace prefix="O"?><o:p></o:p></span></em>
    </p>
    
    <p>
      <em><span><span>(2)<span>&nbsp;&nbsp; </span></span></span><span>Create a<br /> new C# project somewhere called <span class="SpellE">MyApp</span>.<o:p></o:p></span></em>
    </p>
    
    <p>
      <em><span><span>(3)<span>&nbsp;&nbsp; </span></span></span><span>Use<br /> notepad to edit <span class="SpellE">MyApp.csproj</span>. Replace the entire<br /> <Import> tag with <o:p></o:p></span></em>
    </p>
    
    <p>
      <em><span><span>&nbsp; </span></span><span><Import Project=&#8221;$(<span class="SpellE">MSBuildExtensionsPath</span>)\<span class="SpellE">CrossCompile.CSharp.targets</span>&#8221;<br /> /><o:p></o:p></span></em>
    </p>
    
    <p>
      <em><span><span>(4)<span>&nbsp;&nbsp; </span></span></span><span>When<br /> prompted, reload the project. You’ll have to answer a security<br /> dialog.<o:p></o:p></span></em>
    </p>
    
    <p>
      <em><span><span>(5)<span>&nbsp;&nbsp; </span></span></span><span>In VS,<br /> click the drop-down that says ‘Any CPU’ and select ‘Configuration<br /> Manager’<o:p></o:p></span></em>
    </p>
    
    <p>
      <em><span><span>(6)<span>&nbsp;&nbsp; </span></span></span><span>Under<br /> Active Solution Platform, select <New…><o:p></o:p></span></em>
    </p>
    
    <p>
      <em><span><span>(7)<span>&nbsp;&nbsp; </span></span></span><span>Select<br /> ‘.NET 1.1’ (pretty cool, eh?) and press OK.<o:p></o:p></span></em>
    </p>
    
    <p>
      <em><span><span>(8)<span>&nbsp;&nbsp; </span></span></span><span>Build and<br /> notice error about <span class="SpellE">System.Collections.Generic</span>. This<br /> means its working because generics aren’t supported in<br /> 1.1.<o:p></o:p></span></em>
    </p>
    
    <p>
      <em><span><span>(9)<span>&nbsp;&nbsp; </span></span></span><span>Open <span class="SpellE">Program.cs</span> and delete the line:<o:p></o:p></span></em>
    </p>
    
    <p>
      <em><span>using</span><span><br /> System.Collections.Generic;</span><span><o:p></o:p></span></em>
    </p>
    
    <p>
      <span><em><span>&nbsp;&nbsp;&nbsp;&nbsp; </span>And rebuild.<br /> </em></span>
    </p>
    
    <p>
      <o:p></o:p></span>
    </p></blockquote>