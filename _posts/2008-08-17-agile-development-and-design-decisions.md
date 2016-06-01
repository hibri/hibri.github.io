---
id: 331
title: Agile development and design decisions
date: 2008-08-17T19:15:10+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2008/08/17/AgileDevelopmentAndDesignDecisions.aspx
permalink: /2008/08/17/agile-development-and-design-decisions/
categories:
  - Agile
  - development
---
When to make design decisions is a touchy subject when doing iterative software development.&#160; Ever since starting to do TDD, I’ve seen how TDD can drive the design. I’ve also seen how bad it is when a team gets caught in the trap of doing a big up front design. Two bits of advice that have helped me a lot in my current project are;

Doing the simplest thing that could possibly work

Defer decisions till the last possible moment.

What I’m still trying to learn&#160; is;

What is the simplest thing that could work, but doesn’t increase the cost of change later. What is the simplest thing I could do, but still gives me a foundation to build upon ?

How long can I defer a decision ? How do I avoid leaving a decision till too late ? </p> </p> </p> </p> 

A panel discussion led by Martin Fowler sheds some light on this. [You can watch it here](http://www.infoq.com/presentations/modifiability-fowler "Modifiability? Or is there Design in Agility"), and it is a must see. The panel talks about&#160; these two topics and their experiences.

What I gleaned from this is , doing the simplest thing does not mean doing the stupidest thing. Doing the simplest thing possible is under the constraints of proper separation of concerns, encapsulation and having tests to cover what is written.

Doing the simplest thing does not mean you can dump your business logic, persistance and presentation logic all in the code behind file of an ASP .Net page. Keep doing the simplest thing possible by using existing design patterns that reduce the cost of change later. The simplest thing is not an excuse for writing bad code. Having proper separation of concerns in the design ensures that changes can be made in&#160; the simplest thing that was done earlier without adversely affecting the rest of the system.&#160; 

The domain model should not be aware of the persistance or presentation logic. Design decisions don’t affect the domain model design as frequently as other parts of the system. The domain model reflects the business and the decisions are usually made long before the project is begun. 

Doing the simplest thing that could possibly work usually means, how to persist a certain part of the domain model ? how to present domain model data ? and how to pass the data from the domain model to and from the different layers. It is how to implement a certain business requirement in domain model code.

A key safeguard here is having tests (unit and acceptance tests ).&#160; While doing the simplest thing possible do write good unit tests.

Martin Fowler talks about reversibility in design decisions. A good design decision is one that you can reverse and go back to the point before the decision was made. He stresses encapsulation again.&#160; Design decisions that are encapsulated are not expensive to change. If your persistance medium is changed, this decision should not affect the rest of the system. Proper separation of concerns isolates design decisions. The panel also stresses the importance of spiking. If you have choices to make, try those choices with a scaffold or a simple prototype and explore the options. It’s much more cost effective to make a decision through spiking than to undo a choice made to production code. Again the emphasis is made on tests. Tests protect the system, they tell you how much you are likely to break.&#160; 

During the past week a colleague of mine, did a fairly big refactoring of key parts of the code. He did it in a separate branch, and made sure that all the existing tests passed and wrote new tests where needed. Impressive. His design decisions do not affect the trunk, till we are sure that we are happy with it and it hasn’t broken any part of the system. 

In my current project I defer decisions till the first hint of pain of not making that decision appears. I make&#160; the choice just about when we are starting to hurt by not making it. I keep postponing it till then.

To sum it all up;

Do the simplest thing that could possibly work, do not repeat yourself defer decisions till the last possible moment, but still do write the best code you can, and drive the design with tests.