---
id: 334
title: Branching, Merging and avoiding the pain..
date: 2008-07-27T20:41:29+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2008/07/27/BranchingMergingAndAvoidingThePain.aspx
permalink: /2008/07/27/branching-merging-and-avoiding-the-pain/
categories:
  - Agile
  - development
---
In the past two months I&#8217;ve been introducing new practices to my team. An important one was a branching strategy.&nbsp; My team works on several user stories in a sprint. A sprint lasts 2 weeks ( 10 days).&nbsp; I wanted to release regularly at the end of each sprint.&nbsp; 

Prior to implementing the branching strategy,&nbsp; the team worked off the trunk and released from it.&nbsp; This made the trunk less stable with in-complete features.&nbsp; The code was unit tested but not complete. 

We wanted to have better control of what we were releasing for acceptance testing and to the production environment.&nbsp; Releasing the latest version in the trunk caused in-complete code go into a production environment. The strategy I introduced is <a title="Version Control For Multiple Agile Teams" href="http://www.infoq.com/articles/agile-version-control" target="_blank">explained very well in this article</a>. I highly recommend reading this and using it as a starting point if you are working in an agile manner. 

To summarise;

> All development work is done in a development branch. For example, when developing&nbsp; a story, the work is done in a branch for the story. The branch is merged back into trunk when the story is complete (acceptance tested, unit tested, as long as it has met the requirements and is relatively bug free with no show stoppers).&nbsp; During development the developers working on the story branch pull down from the trunk so that they are always in synch with the trunk. When the story is done, the branch is merged back into the trunk and killed off.&nbsp; Several stories can be in development in parallel branches too.

The advantage of this approach is that the trunk is kept relatively clean and has feature complete code ready to release. This makes life much easier for the testers as they have complete stories to test. 

Now this all sounds fine, but it didn&#8217;t go smoothly as I expected. 

First off, most of my team had a steep learning curve in trying to branch and merge. We were working with TFS (Team Foundation Server) at the time. Creating a branch with TFS was a time consuming task. It took a good 10 to 15 minutes to create a new branch from the trunk and commit it back in to TFS.

The next biggest stumbling block for my team was the actual act of merging. Some found it hard to be disciplined and pull down from the trunk regularly, and to always do this first when merging a branch back into the trunk. 

TFS wasn&#8217;t very helpful in when resolving conflicts, it tends get confused when the merge contained renamed files. 

A drawback of such an aggressive branching strategy was sharing code was hard. Improvements or refactored code made in one branch code not be shared by other branches. The code had to go into the trunk first before being pulled down by the other branches.

So at the end of two months where am I ?

I decided not to branch so aggressively. Each story did not have to have a branch of its own. The general policy when creating branches is;

1. Does the story depend on other stories in development ? If yes, use an existing branch.

2. Will starting a new piece of work impact the release of an existing story ? Will it cause the release of one story to contain an incomplete feature of another story ? If yes, the new piece of work belongs in a new branch.

3. Is the new work a bug fix ? Bug fixes on code already released are always in the trunk.

In general, we have settled on &#8220;work branches&#8221;. Branches that can have independent releasable pieces of work. At most we have two branches at any given point in time. Usually there is a branch with work carried over from the previous sprint and all the new work for the current sprint is done in a new branch.

We also ditched TFS and moved to Subversion. This move was done last week, and my team is still settling into it. Creating branches with subversion is a snap. It was very easy to switch Cruise Control .Net to use subversion. We haven&#8217;t still moved to <a title="Subversion Merge Tracking" href="http://subversion.tigris.org/merge-tracking/" target="_blank">subversion 1.5</a> and have to track the merge revision numbers manually.

&nbsp;

If you don&#8217;t have a branching strategy, first consider if you really need one. If you do, and you are working in an agile manner start off with the approaches in this <a href="http://www.infoq.com/articles/agile-version-control" target="_blank">article</a>. 

1. Enforce strict discipline and synchronise branches regularly.

2.No branch should go without merging back into the trunk at-least once every two days. 

3. Listen to the pain points of the team. 

4.I highly recommend paring with another developer when merging back into the trunk. Have a merge buddy. 

5. Always merge locally and not on the server, run unit tests and then check back in. 

6. The chances of a merge going wrong and loosing both the unit test and&nbsp; the code being tested is very little. A compile error will always spot this. 

7. Run CI on each branch. Treat each branch with the same respect as the trunk.&nbsp; 

8. Don&#8217;t let your team treat a branch as place to check-in untested code. 

9. If your tools are giving you pain, change them.

Most of all listen to the pain the team is having but stick with the process. Don&#8217;t drop it because it&#8217;s hard. 

Listen and adapt.