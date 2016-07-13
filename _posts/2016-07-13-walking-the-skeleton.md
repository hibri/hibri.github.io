---
title: Walking the Skeleton
date: 2016-07-13T19:00:00+00:00
author: Hibri Marzook
layout: post
published: true

categories:
  - Continuous Delivery
  - Contiunous Integration

tags:
  - continous-delivery
  - teams
---

The Walking Skeleton pattern, encourages early delivery, of a minimal system to an environment where a user could potentially use it.

[Alistair Cockburn describes the walking skeleton](http://alistair.cockburn.us/Walking+skeleton), in the context of software as follows;

*A Walking Skeleton is a tiny implementation of the system that performs a small end-to-end function. It need not use the final architecture, but it should link together the main architectural components. The architecture and the functionality can then evolve in parallel*

This post is not about the walking skeleton. It’s about using the delivery of the walking skeleton to surface the dysfunctions  an organisation has, in delivering software.

Many teams struggle with delivery of their first feature. Even when the feature is built, it languishes for days, even weeks before someone uses it and gives feedback. 

Why should we incur such a huge initial startup cost ? 

I’d like to take the analogy of “walking” the skeleton, all the way from a developer’s work station to the user. Here are some roadblocks that stand in the way of walking the skeleton to the user.

Some common roadblocks are;

The shared test environment: This is the only environment available for testing. New and old services are dumped here, because at some point in the past it was a copy of the production environment, and everything has to be tested here.

This dysfunction is a result of not having an automated way to spin up an isolated infrastructure for testing.

The DNS Czar: A single person is responsible for creating DNS entries. Forms have to be filled in triplicate, and a few meetings had before a service can be hosted. This leads to hard coded IP addresses scattered around configuration files.

Again this is a dysfunction of not having an automation first approach.

Fear of the new : A new way of automation or a change to an existing process finds resistance. If the metaphorical skeleton dons a Jet pack, the request is denied. This causes much antagonism between devs and ops. 

This leads to a suboptimal deployment processes, as development teams think of workarounds to get things deployed.

This dysfunction, is a result of a lack of communication between teams, and shared ownership of common code. Teams tend to focus only on their own deliverables.


Lack of a shared deployment pattern : There isn’t a shared deployment pattern across the organisation. There will be isolated examples of great and good enough patterns, but these aren’t shared. Each time something new is deployed the wheel has to be reinvented and a shared delivery framework does not emerge.


In the projects I’ve observed, the first week or more of a new project (a new idea) is spent dealing with these dysfunctions. That is one week without customer feedback loop. It is also one week of wasted productivity.

Being sensitive to and removing the roadblocks that slow down the delivery of a walking skeleton, will help reduce the cost of launching a new idea. 

The ideal goal is to reduce the time and cost of launching a new idea as close to zero as possible.

