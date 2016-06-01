---
id: 321
title: Using NHibernate Profiler with database integration tests.
date: 2009-06-10T17:28:07+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2009/06/10/UsingNHibernateProfilerWithDatabaseIntegrationTests.aspx
permalink: /2009/06/10/using-nhibernate-profiler-with-database-integration-tests/
categories:
  - .Net Data
  - Agile
  - NHibernate
---
[The NHibernate Profiler](http://www.nhprof.com) is a pretty cool tool. If you are using NHibernate and want to see how your application/website uses NHibernate this is what you need. 

But, why wait till you use the whole application to start using the profiler. Why not use it when writing&nbsp; writing tests , while building your mappings and when building your NHibernate queries. It’s really easy to do this.

First, get the NHibernate profiler from [www.nhprof.com](http://www.nhprof.com). Extract the contents to a location. From your test project, add a reference to **HibernatingRhinos.NHibernate.Profiler.Appender.dll** in the NHProf package.

This is my small test class.

<pre class="csharpcode">[TestFixture]
    <span class="kwrd">public</span> <span class="kwrd">class</span> EpisodeTests : BaseTest
    {
        [SetUp]
        <span class="kwrd">public</span> <span class="kwrd">override</span> <span class="kwrd">void</span> SetUp()
        {
            <span class="kwrd">base</span>.SetUp();
            ActiveRecordStarter.Initialize(<span class="kwrd">typeof</span>(Episode).Assembly, <span class="kwrd">new</span> XmlConfigurationSource(<span class="str">"activerecord.xml"</span>));
        }

        [Test]
        <span class="kwrd">public</span> <span class="kwrd">void</span> CanPersistTitle()
        {
            Episode episode = <span class="kwrd">new</span> Episode();
            <span class="kwrd">string</span> expectedTitle = <span class="str">"Dr Who and the Daleks"</span>;
            episode.Title = expectedTitle;
            episode.Save();
           
            Guid savedEpisodeId = episode.Id;
            episode = ActiveRecordBase&lt;Episode&gt;.Find(savedEpisodeId);

            Assert.That(episode.Title, Is.EqualTo(expectedTitle));

        }
    }</pre></p> 

<pre class="csharpcode">&nbsp;</pre></p> 

I’m using Castle ActiveRecord (which uses NHibernate behind the scenes) to demonstrate this. To enable NHProf to profile the test, add a static constructor to the super class , **BaseTest**. In the static constructor, add the following code.

<pre class="csharpcode">HibernatingRhinos.NHibernate.Profiler.Appender.NHibernateProfiler.Initialize();</pre>

Go to where you extracted NHProf and run the profiler exe. Run the test and watch the magic.

[<img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.hibri.net/content/binary/WindowsLiveWriter/UsingNHibernateProfilerwithdatabaseinte_FDC4/image_thumb.png" width="659" height="509" />](http://www.hibri.net/content/binary/WindowsLiveWriter/UsingNHibernateProfilerwithdatabaseinte_FDC4/image_2.png) 

NHProf is now profiling your integration tests. You can leave this running in the background while you are working on the tests. 

You get immediate feedback NHibernate best practice violations, and you can_ **fix them while writing tests**._ You don’t have to wait till deployment to profile your code. Although this doesn’t give the whole picture of how your application is using NHibernate , you still can fix many things early. I highly recommend running NHProf while running automated acceptance test scenarios.

<div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:3916a100-f10a-4ead-859e-089ef55b9710" class="wlWriterEditableSmartContent">
  Technorati Tags: <a href="http://technorati.com/tags/NHibernate" rel="tag">NHibernate</a>,<a href="http://technorati.com/tags/TDD" rel="tag">TDD</a>
</div>

&nbsp;