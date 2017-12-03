---
title: ’Tis the season for release freezes
date: 2017-12-03T20:00:00+00:00
author: Hibri Marzook
layout: post
published: true

categories:
  - Continuous Delivery
  - Contiunous Integration
  - Devops

tags:
  - continous-delivery
  - teams
  - devops


---

It’s that time of the year. The inboxes are full with party invites from HR, the successful raising of £143.40 for Movember and the  numerous out of office notifications from those who have had the temerity to escape to warmer climes.

Amongst all those e-mails, just when you think you can archive it all in one swoop, is one with thse tile expected yet, ominous title “Christmas Release Freeze”.

![](/public/images/release-freezes-are-coming-large.jpg)


This marks the time of the year, when all the good practices followed the rest of the year are thrown out with wild abandon. The meeting invites go out for the “Daily Release CAB Meeting” set for 10:30 am everyday for the rest of December, till January till everyone has sobered up and the New Year’s resolutions kick in. It’s the time of the year when middle managers test the boundaries of the [Peter Principle](https://en.wikipedia.org/wiki/Peter_principle), whilst the higher ups are away. 

It’s the time of the year when the delivery pipeline freezes as the central heating pipes warm up. Nowhere do the Agile manifesto or the Continuous Delivery book does it say, “Applicable between January 8th and November 30th”. 

## The reality of a release freeze
However, the reality is that even during a release freeze, releases still happen, but with more [release management theatre](https://continuousdelivery.com/2013/08/risk-management-theatre/). The daily CAB meetings are spent arguing why one release is more important than the other and should break the rules. 

Woe to the developer who intends to use the downtime to read the Continuous Delivery book. A manager comes over with a bounce in his step, asking to see if the feature that everyone ignored the rest of the year, can be built in the spare time suddenly available because of the release freeze. 

I’ve never observed a successful release freeze, that had zero releases during the release freeze period. The release cadence has always been similar to the rest of year with the extra friction of pointless meetings. 

The argument made for release or change freezes is to maintain stability, whilst having only a skeleton crew to deal with any issues. The holiday period is when organisations see their largest transaction volumes for the whole year. The need for stability is valid one. 

## What are the alternatives?
A business powered by technology doesn’t stop whilst the release freeze is in place. Why should we freeze change of technology that powers the business?
Let’s look at a few methods to overcome the madness that is a release freeze

### Slowdown instead of freezing
Instead of coming to a complete stop, slow down the pace of work. If you’ve been continuously delivering change the rest of the year, at a faster pace, then it should easy to slow down. 
Doing work in smaller batch sizes allows you to be reactive quickly. They also have less risk, and it’s easier to assess the risk of a small change upsetting the stability of a system. 
  
Smaller items can be released by a skeleton team, in a serial manner. It gives them time to focus on the work, without the extra noise that is present around a team the rest of the year. Anecdotally, I’ve seen teams be more productive during the holiday period.

The hard truth is that, many organisations find it hard to slow down. The software delivery process is optimised for large pieces of work and big bang releases. Release management theatre does need a large audience!

### Prioritise stability and resilience
If you care about stability, you should care about it the whole year and not just during the last month of the year. Work on resilience. A resilient system and process will scale up and down according to the demand placed on it. 

To help with building resilience, add good alerting and monitoring to the applications you build. This helps a skeleton team during the holiday period deal with any unexpected issues without having to rely on someone who is away on holiday. 

### Don’t start new work
Avoid the temptation to use the newly found free time to start working on major features. This causes more risk to be piled up waiting to be released, and potentially blow up when the release freeze is lifted. Some developers can be overly bold and daring after the office Christmas party drinks and implement major features. Only to have very little recollection of what was done the next year. 

Management tends to have the temptation to take advantage of large transaction volumes. If you do intend to do this. Plan for it, and do the change earlier, and have it ready before the release freeze. Avoid rushing in the quick hacks. They will come haunt the system for many years.

### Accept the release freeze 
Finally, you can always accept there is a release freeze. It provides precious slack time for learning. Use the time to do code katas and encourage the them team to use the quiet uninterrupted time to read, tinker and play with technology (as long as it’s not with a system in production). The learning will help the organisation build a better system next year. 

The slack time gives a mental reprieve from the fast pace during the rest of the year. It will help them recharge, and bring in fresh ideas. Long lasting change happens during slack time. 

Adopting Continuous Delivery practices helps to build a system and delivery process that can scale up or down according to the needs of the business, which the technology powers. Smaller pieces of work have less risk than larger pieces of work. During the rest of the year the organisation can deliver smaller pieces of work at a faster pace, and still keep delivering with little risk during a critical part of the year.



