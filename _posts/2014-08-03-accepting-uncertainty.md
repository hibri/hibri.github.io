---
id: 1345
title: Accepting Uncertainty
date: 2014-08-03T11:53:03+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/?p=1345
permalink: /2014/08/03/accepting-uncertainty/
categories:
  - Agile
  - Continuous Delivery
---
This is one of those things that should be filed under continuous delivery patterns. One of the anti-patterns I see in continuous deployment, is the need to make sure that the software is flawless before it&#8217;s released. This anti-pattern manifests itself, in the need to have several stakeholders test and approve a release. The release dance takes days, when something is good enough to be on a production system.

There is a large suite of long running tests that must be run, before a release is approved. There is a release management dance that _**must be done**_ before a release. Cue the constant conversations around the office about the impending release.

Instead, let&#8217;s accept the inherent uncertainty in building software. Any non-trivial system is complex. We can&#8217;t predict it&#8217;s behaviour to any accuracy. We can only observe and react to any unexpected behaviour.

This is the key tenet in building a continuous deployment pipeline. The ability to react to uncertainty.

Chasing certainty with more automated tests will only give diminishing returns. There should be enough tests to increase the confidence level. That&#8217;s it. Nothing more.

The rest comes from observing how the software behaves. By monitoring and gathering data. Use that,  to react. Add a few more tests. Rinse, repeat. Iterate.

The ability to iterate and react will give better quality software in the long term, than a stranglehold with tests and testers.

&nbsp;