---
id: 3166
title: Getting started with Windows Containers
date: 2016-05-22T17:58:03+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/?p=3166
permalink: /2016/05/22/getting-started-with-windows-containers/
medium_post:
  - 'O:11:"Medium_Post":11:{s:16:"author_image_url";s:69:"https://cdn-images-1.medium.com/fit/c/200/200/0*9AlhGwCMOXvvLqRu.jpeg";s:10:"author_url";s:25:"https://medium.com/@hibri";s:11:"byline_name";N;s:12:"byline_email";N;s:10:"cross_link";s:3:"yes";s:2:"id";s:12:"1c7497872659";s:21:"follower_notification";s:3:"yes";s:7:"license";s:19:"all-rights-reserved";s:14:"publication_id";s:2:"-1";s:6:"status";s:6:"public";s:3:"url";s:78:"https://medium.com/@hibri/getting-started-with-windows-containers-1c7497872659";}'
categories:
  - Continuous Delivery
  - Contiunous Integration
---
Earlier this year Microsoft announced Windows 2016 Server TP-5 with support for Windows Containers.

Windows Containers allows a server to act as  container host for containers that can be managed with tools like Docker.  However, a Windows container host can run only Windows containers, and not Linux containers.

I work on a Mac, and I want to use the Docker client on OSX to build Windows Containers. Here is what I went through to set up my environment to start playing with it.

## Step 1

Build a virtual machine with the latest Windows 2016 Technical Preview (TP5 at the time of writing).

The usual way is to download, mount the iso in VirtualBox or VMware Fusion and install. After the installation, follow the quick start instructions to configure Windows Containers.

The quick start guide is at [https://msdn.microsoft.com/en-us/virtualization/windowscontainers/quick\_start/quick\_start\_configure\_host](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/quick_start/quick_start_configure_host)

My preferred method is to create a Vagrant box, so that I can have a repeatable base build to experiment on.

Packer is the tool to build Vagrant boxes. There exists a [Packer Windows project](https://github.com/joefitzgerald/packer-windows) to build vagrant boxes. The main Packer Windows doesn&#8217;t contain templates for Windows Server 2016 yet. [Stefan Scherer](https://github.com/StefanScherer) has been working on supporting it, and has built templates to provision container hosts as well. Clone the Packer templates from <https://github.com/StefanScherer/packer-windows>, and run

<pre style="padding-left: 30px;">packer build windows_2016_docker.json</pre>

This tells packer to build a Vagrant box with Windows 2016 TP5 as a container host.

Once the box has been built, copy it to a place where it can be reused. My preferred place is a private Dropbox. You&#8217;ve now got a Vagrant box acting as a Windows Container Host, ready to experiment with.

## Step 2

Spin up the Vagrant, Windows Container Host box by creating a Vagrant file

<pre style="padding-left: 30px;">vagrant init -mf  windows_2016_docker &lt;url to your vagrant box&gt;</pre>

Start the Vagrant machine by running

<pre style="padding-left: 30px;">vagrant up</pre>

Wait till the Vagrant machine starts up.

## Step 3

Connect the Docker client to the Vagrant machine running the Windows Container Host.

When the Vagrant machine starts up, it will display the IP address of the Vagrant machine. Use this IP address to set the **DOCKER_HOST** environment variable to tcp://<ipaddressofcontainerhost>:2375

In my environment it&#8217;s done by running,

<pre style="padding-left: 30px;">export DOCKER_HOST=tcp://192.168.3.144:2375</pre>

<pre>Then run  <strong>docker version</strong> and look at the output. It should be something like the following.</pre>

<pre style="padding-left: 30px;">Client:
 Version: 1.11.1
 API version: 1.23
 Go version: go1.5.4
 Git commit: 5604cbe
 Built: Wed Apr 27 00:34:20 2016
 OS/Arch: darwin/amd64

Server:
 Version: 1.12.0-dev
 API version: 1.24
 Go version: go1.5.3
 Git commit: 2b97201
 Built: Tue Apr 26 23:51:36 2016
 <strong>OS/Arch: windows/amd64</strong></pre>

&nbsp;

The OS/Arch value should tell you that the Docker client on OSX, is connects to a Windows Host.

## Step 4

Create a [Dockerfile](https://docs.docker.com/engine/reference/builder/), with the following content.

<pre style="padding-left: 30px;">FROM windowsservercore
RUN powershell.exe Install-WindowsFeature web-server
EXPOSE 80</pre>

This creates a Windows Docker Container image, using Windows Server Core as the base image, installs IIS, and exposes port 80

Build the Dockerfile.

<pre style="padding-left: 30px;">docker build -t iis .</pre>

And run the image with

<pre style="padding-left: 30px;">docker run --name iisdemo -d -p 80:80 iis</pre>

That&#8217;s it. You now have a container running IIS. Visit http://<ipaddressofcontainerhost> to see the familiar IIS start page.

## Summary

You&#8217;ve now got an environment to start experimenting with Windows Containers and Docker. You can start writing Docker files for your Windows only applications, and even start  porting .Net services to run on Windows Containers.

&nbsp;