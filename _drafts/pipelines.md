---
title: A model for building and thinking about pipelines
date: 2019-03-04T00:00:00+00:00
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
# What is a good software delivery pipeline?

Delivery pipelines are a critical part of the software delivery life-cycle. In this post I look at what makes a good delivery pipeline.

A delivery pipeline it’s not just to deliver the code we built blindly to the user. It’s a vehicle for getting feedback and finding better ways to build the product. In addition, the way pipelines are created are a result of how everything outside of the pipeline is. Such as organisational structure and ways of working. 

Pipelines tend to be a reflection of the organisation’s practices. In a technology driven org, pipelines reflect the value stream. They encapsulate the activities the organisation does to build and deliver software successfully.

To help with assessing the design of a pipeline, I propose the following model;

A pipeline helps us reduce risk as we traverse it.
A pipeline helps us test for these risks and give us an early opportunity to mitigate them.

With this model overtime, the team should;
1.  aim to reduce the the time to get feedback. 
2.  aim to test for known risks earlier, ideally towards the left. 
3.  aim to build mechanisms to discover unknown risks and turn them into known risks.

We can’t address all risks in the pipeline. We can test for known risks, and build up our knowledge to address them in the future in the form of tests.

(word this better)
Tests are our archive of known risks. When we un-cover an unknown risk we fix our system to mitigate it, and test if we’ve successfully mitigated against it. 

Now that we’ve got a model for what a good pipeline looks like; let’s see how to apply it to building pipelines.


The dev’s workstation is where the pipeline starts. 
(diagram showing tasks on dev box, feedback loop under minutes)

## The creation context
A developer should be able to checkout a source control repository and get a green build, with all tests passing. The developer should not have to spend days getting the development environment ready to work on a project.

1. Run compilation, listing and syntax checks.
2. Run unit tests
3. Run integration tests
4. Run acceptance tests, with mocks and stubs in place.
5. Be able to run replicate the production system, with production like data (or have the ability to generate data)
6. Be able to run any stage in the pipeline (other than deployment) locally.
7. Be able to work in a disconnected mode ( the work from train mode)
8. Be able to run  tests in parallel or continuously

All of the above should be achievable in a matter of seconds or minutes (not more than 10 minutes), and be able to be replicated consistently. (See automating dev workstations)

Above all optimise for developer productivity.

All of the above should be able to run on a CI/CD server as well. 

## The collaboration context 

 The next stage is in the pipeline is preparing for collaboration with others who are working on the same system. This means ensuring my code is ready to be integrated with what everyone else has done, and also does not break (or fixes what is broken) what is already there. 
 We commit and push our changes to the source control repository, this should trigger a CI/CD build.
 
 We run all the steps that run on the dev’s workstation, just to ensure that it doesn’t just “Works on my machine”
 
 This should signal to the rest of the team, that there is something new is available to integrate. We do code reviews and obtain feedback on the code that’s been written. Expect to do changes at this point. Stay with the code till it’s been integrated.
 
 
## The fit for purpose context (another name ?)

The next stage is to find out if what we’ve built is fit for purpose. This is where the feedback loop gets a longer. 

We run acceptance tests, security checks, security pen-tests, and performance tests. 
This is where we run tests on the whole system from the outside. Unit tests which are run earlier in the pipeline look at the internals of the system.




## The deployment context

## The release context

## The feedback context







e