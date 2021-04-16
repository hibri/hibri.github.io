---
title: "How to create a secure and postive Developer Experience on Azure"
author: Hibri Marzook
layout: post
published: true
date: 2021-04-16T15:00:00+00:0

categories:
  - Azure
  - DevEx
  - Cloud

tags:
  - Cloud
  - Azure
  - devex

---

An anti-pattern I've seen in security-conscious organisations is, access to the Public Cloud provider's console is restricted in development environments. In a recent project I worked on, developers did not have access to the Azure portal to view, debug and test changes in a non-production environment. The restricted access impeded the developer experience (DevEx), negating the Public Cloud's productivity benefits. 

Let's look at how we can safely improve the developer workflow and mitigate the risks associated with giving developers more autonomy.

## The problem - restricted developer experience

Access to the portal was given only to the Ops team. The team did not have access to the Azure subscription through the Azure portal to verify changes or debug problems. The team had to engage the Ops team to look at the problem, usually via raising a ticket and then explaining the problem and waiting for a response. 

This mode of working is a DevOps anti-pattern. A developer should have the freedom to resolve their issues without having to depend on another team.

The handoff creates a significant delay in the development workflow. It increases the development cycle from minutes to hours and days. The long debugging cycle and handoffs incur costs on both the development team and the Ops team. 

The developer is blocked, and the wait-time increases development costs. An Ops team member has to be interrupted to un-block a developer. Resources are diverted from making platform improvements, creating a negative loop. I call this the Wall of Confusion.

![Restricted Developer Experience - Wall of Confusion](/public/images/2021-04-16-wall-of-confusion.png)


## What should an ideal developer experience look like?

The developer writes infrastructure as code (IaC) to create and configure Azure. The developer checks in code and tests to source control. The code commit triggers a pipeline, which runs the IaC to make the intended changes first in the development (Dev) environment.

The pipeline then executes the tests automatically to test for regression and that the new functionality works. When the tests pass (the build is green), the changes are propagated to the following environment. 

![Unrestricted Developer Experience](/public/images/2021-04-16-dev-workflow.png)

In the Dev environment, a developer will need to eyeball the changes made to Azure resources to verify that the resources were created and configured as expected. 
A successful run of the pipeline may not always indicate a successful deployment. 

If a test fails, the developer will need to use the Azure portal to check the state of resources related to the failure. The developer should also have access to manually create new resources to test the latest changes before applying the fix to code and committing the change to source control, which triggers the pipeline.

The developer goes through the development workflow described above many times (minimum of 50 to 100 times) a day and runs through the whole workflow in minutes. The quality of the system is improved when the developer has a fast feedback loop.

## The impact of a poor developer experience

Cochran (2021) shows a simple representation of how developers use feedback loops and a comparison of the time taken for developer activities in the restricted (low-effective) environment and un-restricted (high-effective) environment. 

![Feedback Loops during feature development (Cochran, 2021)](/public/images/2021-04-16-feedback-loops.png)

The important observations are;

* Developers will run the feedback loops more often if they are shorter
* Developers will run tests and builds more often and take action on the result if they are seen as valuable to the developer and not purely bureaucratic overhead
* Getting validation earlier and more often reduces the rework later on
* Feedback loops that are simple to interpret results, reduce back and forth communications and cognitive overhead

## How to improve the developer experience safely?
So how do we improve the developer experience whilst keeping production data and sensitive configuration secure?

We need to start with some. Restrictions.
Developers will **only** have permissions to view, manage and debug resources via the Azure Portal in lower environments such as Dev and Test. 

Developers will **only** have read-only access in higher environments, such as Pre-Prod and Prod, for the following;

* Monitor application health and alerts
* View resource costs and budget limits
* Error messages and logs

Developers **will be not** be given permissions to view the following in higher environments;
 
* Sensitive configuration settings
* Data in databases
* Key vault secrets 
* Logs with sensitive data

We leverage Role-Based Access Control (RBAC) to manage access. Here's an example using Azure's built-in roles.

![Levels of access across environments](/public/images/2021-04-16-portal-subscription-rbac.png)

The built-in Azure roles, which will be assigned to the user group that the developer is in. It's expected that the RBAC assignments will be at the management group level and not at the subscription level.

To make this work, subscriptions are associated with product team-specific Azure management groups to ensure proper configuration and control of subscriptions.

The **only** path to a Production environment will be via pipelines in Azure DevOps, using code from source control. Changes made via the portal **will not be** propagated to higher environments and can be overwritten on the next pipeline run.

## Mitigating the risks associated with the approach

There are common arguments against the approach described above and the risks associated with it. However, there are effective mitigations.

1. **A developer can accidentally destroy resources belonging to other teams**. We mitigate this risk by scoping Contributor access only to the product team-specific Azure development subscription, and mistakes are not propagated to other teams. The team should be able to re-create resources from source control.
2. **Shared platform components can be deleted**. Again, this risk is mitigated by having dedicated subscriptions for shared platform components. Only the teams responsible for those components have access.
3. **A developer can accidentally expose data to the Internet**. We mitigate this risk by having guardrails using Azure Policy, which are applied at the management group level. The policy prohibits the creation of resources that will allow data egress to the Internet. We allow ingress and egress to only via shared services, which have the appropriate governance built into them. There should also be no live data in a development environment.
4. **Developers will be able to modify production infrastructure**.  Azure Portal access in higher environments is read-only and restricted to observability. Temporary break-glass access to Prod is catered to through Azure Privileged Identity Management.
5. **Costs could increase if developers can create resources**. Subscriptions are assigned to product teams, who will own the cost of running the subscription. When developers have access to the billing dashboard, they can self manage expenses. **The cost of lost developer productivity is often greater than the cost of infrastructure**.

## What do we get when we unblock the developer experience?

Adopting the approach has positive benefits, even though managing RBAC at scale requires extensive automation.

* The developer experience is positive and creates a **high effective environment**. A **highly effective environment** is where there is a feeling of momentum; everything is easy and efficient, and developers encounter little friction
* Product teams can launch new services quickly
* The developer can observe the application in a production environment, creating a feedback loop that reinforces a positive culture
* The developer can take advantage of existing Azure knowledge and familiarity with the Azure Portal to diagnose problems independently

## References

Cochran, T. (2021) Maximizing Developer Effectiveness. Available at: [https://martinfowler.com/articles/developer-effectiveness.html](https://martinfowler.com/articles/developer-effectiveness.html) (Accessed: January 11, 2021)

