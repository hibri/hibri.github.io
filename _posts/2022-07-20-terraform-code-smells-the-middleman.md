---
title: "Terraform Code Smells - The Middleman"
author: Hibri Marzook
layout: post
published: true
date: 2022-07-20T15:00:00+00:0

categories:
  - Terraform
  - Cloud

tags:
  - terraform
  - refactoring
  - design

---

Infrastructure as Code has [code smells ](https://en.wikipedia.org/wiki/Code_smell)(its code too !!) and as we work more with it, it's important to be aware of code smells that indicate a deeper problem.

The [Middleman](https://refactoring.guru/smells/middle-man) doesn't do anything other than delegate to a native resource

Let's look at an example;

```
module storage_account {

	source = "./module/resource-group"

	name = var.storage_account_name

	resource_group_name = var.resource_group_name

	location = var.location

	account_tier = var.account_tier

	account_replication_type = var.account_replication_type

	tags = {

		environment = "staging"

	}

}
```

Here we see a module that creates a storage account. Let's look inside the module itself.

```
  
resource "azurerm_storage_account" "storage_account" {

	name = var.storage_account_name

	resource_group_name = var.resource_group_name

	location = var.location

	account_tier = var.account_tier

	account_replication_type = var.account_replication_type

	tags = var.tags

}
```

The module has a single resource. The variables are delegated to the resource. There are no collaborating resources inside the module.

## Why is this a code smell?

The module itself does not add any value over using the native resource directly, and is a thin wrapper around the single resource. A Terraform module is a group of resources that work together cohesively.

This code smell appears because of the need to control what types of resources are used in the organisation's context. We can use [Azure Policy](https://docs.microsoft.com/en-us/azure/governance/policy/overview) and [AWS Guardrails](https://docs.aws.amazon.com/controltower/latest/userguide/guardrails.html) to achieve the same result

Another reason is the need to deploy resources consistently across the organisation. For example, to apply tags consistently. Again we can use policies to enforce consistent rules. 

Does it satisfy the five [CUPID properties](https://dannorth.net/2022/02/10/cupid-for-joyful-coding/)? 

* **Unix philosophy:** Does it do one thing well? it does, but all it does is delegate. The work is done by the resource that is wrapped in the module
* **Predictable:** Does it do what you expect? It's unclear why a module is used than using the resource directly
* **Idiomatic**: Does it feel natural? It introduces an extra level of in-direction compared to using the resource directly
* **Domain-based:** does the solution model the problem domain? The module doesn't model the domain, it duplicates what Terraform does

## Treatment

Avoid wrapping single resources with modules. Terraform modules are composed of resources that work together to provide a cohesive building block. Get rid of the middleman.

