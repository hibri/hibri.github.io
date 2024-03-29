---
title: "Terraform Code Smells - The Confused Module"
author: Hibri Marzook
layout: post
published: true
date: 2022-07-01T15:00:00+00:0

categories:
  - Terraform
  - Cloud

tags:
  - terraform
  - refactoring
  - design

---


Infrastructure as Code has [code smells ](https://en.wikipedia.org/wiki/Code_smell)(its code too !!) and as we work more with it, it's important to be aware of code smells that indicate a deeper problem.

A Confused Terraform module has parameters, that change the behaviour of the module. Different parameter value combinations allow the behaviour to change. The module is confused about its identity.
Let's look at an example;

```terraform
module "secure_vpc" {

	source            = "./aws_vpc"
	name              = "mysupersecurevpc"
	range             = "192.168.0.0/24"
	region            = "us-east-1"
	allow_egress      = true
	enable_monitoring = true
}

```

This is an example of a module that creates a VPC. The module declaration has parameters that change its behaviour.  There is the option for the VPC to allow egress outside the network, and the option to turn monitoring on or off.
This is a simple example, but modules tend to have long lists of parameters, with switches that change the module's behaviour. A consumer of the module has to specify the right combination of switches for the behaviour they want.

![switches.png](/public/images/2022-07-30-terraform-smells-confused-module-switches.png)

## Why is this a code smell?

The default behaviour of the module isn't clear, without reading the documentation (or the code for the module). It's easy to accidentally allow egress and deploy the VPC to an insecure state. If allowing egress implies that monitoring is turned on (to make sure that traffic that goes out of the network is monitored), the optional 'enable_monitoring' flag needs to be set. The onus is on the consumer of the module to ensure that the VPC is deployed in a compliant state.

The switches in the parameter list proliferate into the code, and each time we add a new capability we have to guard against breaking existing capabilities.

Does it satisfy the five [CUPID properties](https://dannorth.net/2022/02/10/cupid-for-joyful-coding/)? 

* **Unix philosophy:** Does it do one thing well? The module has multiple behaviour depending on the combination of switches
* **Predictable:** Does it do what you expect? It's easy to accidentally deploy the module in a non-compliant state
* **Domain-based:** does the solution model the problem domain? It's not clear what this module offers over a the out of the box aws vpc resource

## Treatment

Create modules that encapsulate the behaviour rather than make it optional.
For example;

```terraform
module "secure_vpc_with_egress" {
	source            = "./aws_vpc_with_egress"
	name              = "mysupersecurevpc_with_egress"
	range             = "192.168.0.0/24"
	region            = "us-east-1"
}


module "locked_down_vpc" {
	source            = "./aws_locked_down_vpc"
	name              = "mysupersecurevpc"
	range             = "192.168.0.0/24"
	region            = "us-east-1"
}
```

In the example, we've created a module that is explicit about its behaviour. A consumer of the module is clear about what it does and doesn't have a choice of turning monitoring on or off. There isn't the option to deploy the module to an insecure state. 

Each module now does one thing well, and it's behaviour is predictable. The name of the module describes the behaviour in the context that it's being used.

Both modules can now evolve without having to worry about breaking the functionality of the other.


