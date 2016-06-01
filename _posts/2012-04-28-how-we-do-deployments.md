---
id: 568
title: How we do deployments at 7digital.
date: 2012-04-28T16:44:08+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/?p=568
permalink: /2012/04/28/how-we-do-deployments/
categories:
  - .Net General
  - .Net Web
  - Agile
  - Contiunous Integration
  - TDD
---
At 7digital, deployments to a production environment are a non-event. On a given day, there can be at least 10 releases to production during working hours. On some days even more. Specially on Thursdays before the 4pm cut off, as we don’t deploy to production after 4pm and on Fridays.&#160;&#160; 

Deployments to our internal testing environments happen constantly, on every commit. I’m able to deploy a quick fix, or patch something in production without having to make changes on a live server. We rarely roll back, instead roll forward by fixing the issue. This is made possible due to our investment in build and deployment tools. We attempt to treat these with the same care as our production code.

This post is about how it works. 

### A little bit about our stack. 

Our services run on the .Net stack, with SQL server back ends mostly. We use IIS 7and IIS 6, load balanced&#160; behind [HAproxy](http://haproxy.1wt.eu/).

We use [Teamcity](http://www.jetbrains.com/teamcity/), to trigger Rake scripts, to do our deployments. The [Albacore gem](https://github.com/derickbailey/Albacore) is used for the majority of tasks. We use code derived from [Dolphin deploy](https://github.com/BenHall/DolphinDeploy) to configure IIS.

&#160;

### In the beginning.

We used MSBuild for building our solutions and deploying software. However, this was very painful, and led me on a personal crusade to get rid of Msbuild for deployments.&#160; XML based build frameworks, limit what you can do to what is defined in the particular framework’s vocabulary. A big pain was having to store configuration and code in the same msbuild xml files. It wasn’t possible to separate the two without writing custom tasks. 

A build framework, in a programming language, allows you to be much more fluent and write readable scripts. You have the power to use all the libraries,&#160; at your disposal to write deployment code instead of being limited to a XML schema definition. In addition to Ruby, we have&#160; a couple of projects using Powershell and psake.

### &#160;

### The current setup.

&#160;

[<img style="background-image: none; border-right-width: 0px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto; padding-top: 0px" title="deployment" border="0" alt="deployment" src="http://www.hibri.net/wp-content/uploads/2012/04/deployment_thumb.png" width="554" height="429" />](http://www.hibri.net/wp-content/uploads/2012/04/deployment.png)

&#160;

The diagram above shows the major parts of our deployment pipeline. 

We keep the build and deployment code along with the project code, to maintain a self contained package, with minimal dependencies on anything else.

A project has a master rake file, named rakefile.rb in the root directory of the project. This rake file references all the other shared rake scripts and ruby libraries needed for build and deployment. 

These libraries and scripts are kept in a sub directory named build. A typical project structure is like;

_root   
&#160;&#160;&#160; build   
&#160;&#160;&#160;&#160;&#160;&#160;&#160; conf   
&#160;&#160;&#160;&#160;&#160;&#160;&#160; lib   
&#160;&#160; src   
&#160;&#160;&#160;&#160;&#160;&#160; XX.Unit.Tests   
&#160;&#160;&#160;&#160;&#160;&#160; XX.Integration.Tests   
&#160;&#160;&#160;&#160;&#160;&#160; XX.Web_

The conf directory contains the configuration settings for IIS, including the host headers, app pool settings and .net framework version settings.

The [Albacore build](https://github.com/derickbailey/Albacore "Rake tasks for .Net") gem has everything that is needed to build a .Net solution. We use it to compile our code on Teamcity and to run our tests.

When something is checked into VCS (git), Teamcity triggers off a build and compiles the code. This build process will package the deployment scripts and the web site package, which will be used for deployment. Teamcity stores these as artefacts, and this allows us to reuse them without building again.

To deploy a website, a Teamcity build agent, retrieves all necessary zipped packages, un-compresses them to the current working directory.

The build agent calls a rake task, with the parameters;

&#160;&#160; rake deploy[environment, version\_to\_deploy, list\_of\_servers, build_number]

An example

&#160;&#160; rake deploy[“live”,”1.2”,”server1;server2;server3”,”123”]

The environment parameter specifies which deployment settings to use.&#160; Deployment settings are stored in&#160; YAML files, that the rake scripts read.&#160; A YAML file for IIS settings looks like;

<pre class="csharpcode">uat:
 site_name: xxx.dns.uat
 host_header: 80:xxx.dns.uat:*
                        443:xxx.dns.uat:*
 dot_net_version: v4.0

live:
 site_name: xxx.dns.com
 host_header: 80:xxx.dns.com:*
                        443:xxx.dns.com:*
 dot_net_version: v4.0</pre>

&#160;

We can add a new environment, and change settings for an existing environment by changing a configuration .yml file, without having to change deployment scripts. 

The version\_to\_deploy parameter, loosely translates to a virtual directory. This is ignored for websites that deploy to the root. The list of servers is an arbitrary list of servers that we deploy to. This allows us to deploy to a single server or a cluster.

The rake deploy task, calls two other rake tasks, for each server in the list of servers. The first task is to copy all deployment scripts and the web package to the target server. The second is to trigger a remote shell command to do the actual installation process.

In pseudo code

&#160; _deploy
      
  
&#160;&#160;&#160;&#160;&#160;&#160; foreach(server in servers) </p> 

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; copy scripts and packages to server 

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; trigger remote installation</em> on server&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; 

The actual installation process does not happen from the build agent, but on the target server. The build agent does not have the the necessary network access and admin rights. Our servers expose only SSH. 

The deployment sequence is controlled by chaining rake tasks. This allows us to run any of the tasks individually from the command line to do a manual deployment or to test.

The remote installation task, copies all the web site binaries to the correct locations under IIS, and configures IIS. Application pools under IIS are stopped, while this happens, and the virtual directory and if needed the web site are rebuilt. The application pools are restarted after this.

The deployment&#160; repeats the process on the next server in the list. 

&#160;

### The future.

What we have now helps us a lot, and allow us to scale up to this point. However, to grow even more there are a few things that hold us back.

For example, a lot of infrastructure details creep into our configuration and scripts and stored in source control, which is mostly used by devs. This means that&#160; when our operations folk make a change to the infrastructure the devs have to change our configuration settings to reflect this. I would like to have all configuration settings stored somewhere, and the scripts would call out to a service to get all the settings for a particular environment and application. This service would be maintained by devops, and will be synchronized with changes made to the infrastructure.

The same can be done for the list of servers. Instead of a developer having knowledge of what servers comprise an environment, the script could ask the same service, to give a list of servers that are in a given environment. This will allow us to scale transparently, by adding a new server to the list and doing a fresh deploy.

&#160;

### Summary.

I’ve tried to capture an overview of how we deploy our software at 7digital. There is a lot of detail I haven’t gone into. Especially the nitty gritty of setting up IIS host headers, ports and app pool settings. A build and deployment framework is something we do from day one of any new project. We make sure that we have a skeleton application deployed all the way to production before any new code is written.

Feel free to get in touch if you have any specific questions.

Resources:

[http://codebetter.com/benhall/2010/10/22/dolphin-deploy-deploying-asp-net-applications-using-ironruby/](http://codebetter.com/benhall/2010/10/22/dolphin-deploy-deploying-asp-net-applications-using-ironruby/ "http://codebetter.com/benhall/2010/10/22/dolphin-deploy-deploying-asp-net-applications-using-ironruby/")

[http://albacorebuild.net/](http://albacorebuild.net/ "http://albacorebuild.net/")