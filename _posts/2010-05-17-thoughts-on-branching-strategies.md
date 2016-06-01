---
id: 314
title: Thoughts on branching strategies.
date: 2010-05-17T21:00:42+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2010/05/17/ThoughtsOnBranchingStrategies.aspx
permalink: /2010/05/17/thoughts-on-branching-strategies/
categories:
  - Agile
  - development
  - TDD
---
There comes a time during every project, when someone in the team asks the question “What is our branching strategy? “. Off we go trying to find out what is the current branching best practice, what are other teams using ? , What is the Agile way ? We may find solutions in <a href="http://martinfowler.com/bliki/FeatureBranch.html" target="_blank">feature branching</a>, per story branches, <a href="http://svnbook.red-bean.com/en/1.5/svn.branchmerge.commonpatterns.html" target="_blank">release branches</a> and so on.

Let’s take a step back. Why do we need a branching strategy ? What is a branch ?

We want to put some code in a source control branch, because the code contains the risk of breaking the software in the mainline of development, trunk. 

Are we 100% sure that the code in the branch won’t break what is in trunk ? We won’t know for sure till we integrate the branch with trunk.&#160; We won’t know, until it goes through automated/manual testing, and all this after going through merge hell.

We put code in a branch to reduce risk. However, we haven’t reduced that risk. The risk is still there, and we bring it back into trunk. Why not look at methods of reducing the risk in the first place ? 

How do we reduce risk ?

**1. Cut up a big piece of risk into smaller pieces of risk.** 

The bigger the risk the more chopping it needs. Now we have smaller things to work on. We do those small pieces one by one, and if something breaks, we know which change broke it. Easier to fix because it was a small change. 

**2. Break down a big piece of risk, into parts that have no risk and parts that have risk.** 

Analyze the problem, break it out in to parts that can be done without breaking our software. This is interesting. The part which we thought would be a problem might have become a non-issue. We’ve isolated it. We know exactly which change will break our software. See 1 above

**3. Write tests for things that can be broken by the risky bit of code and continuously test.** 

We know what could break, by the new change. Before we make the change, let’s write tests for our software so we know when it is broken.&#160; Let’s make a change. Is anything broken ? No. Did the next change break it ? yes. Fix it. Keep going.

Instead of shoving off our risky code into a branch, we’ve learnt to manage the risk, and reduce it. If the risk is so high that we can’t mitigate it by doing 1,2 and 3, then let’s create a branch for the code. We have a branching strategy based on risk. We create a branch only for code that is riskiest, and we haven’t been able to reduce that risk by a divide and conquer approach.

In my opinion this is a much better way than having a default branching strategy for every piece of work/story/feature/MMF. Working continuously on trunk has benefits. We can release a feature faster, get refactoring changes others have made quicker. Not go through merge hell, and risk loosing code in the process. Along the way we’ve learnt how to break up a problem into smaller pieces. We’ve got better at writing tests. We’ve learnt how to structure our software so that one thing does not break everything else and we get closer to the nirvana of <a href="http://toni.org/2010/05/19/in-praise-of-continuous-deployment-the-wordpress-com-story/" target="_blank">continuous deployment</a>, because we have only one production line of code to deploy from.

Do you need a branching strategy ? Think again.

&#160;

&#160;

<div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:f6aa0a36-a879-49f6-afe1-ead4480d5b94" class="wlWriterSmartContent">
  del.icio.us Tags: <a href="http://del.icio.us/popular/%22branching+strategies%22" rel="tag">"branching strategies"</a>,<a href="http://del.icio.us/popular/%22agile+branching%22" rel="tag">"agile branching"</a>,<a href="http://del.icio.us/popular/branching" rel="tag">branching</a>
</div>