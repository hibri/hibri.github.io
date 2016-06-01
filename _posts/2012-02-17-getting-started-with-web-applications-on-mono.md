---
id: 546
title: Getting started with web applications on Mono
date: 2012-02-17T13:14:59+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2012/02/17/getting-started-with-web-applications-on-mono/
permalink: /2012/02/17/getting-started-with-web-applications-on-mono/
categories:
  - .Net Web
  - development
---
&#160;

I’ve started to explore mono, with a view to moving some of our web applications to Linux. Used MonoDevelop&#160; on OSX to&#160; spike a simple HttpHandler to return a response.&#160; I was more interested in how the hosting and deployment story worked with mono.

This is a little list of things I discovered as I went along.

<http://www.mono-project.com/ASP.NET> has&#160; list of the hosting options available.&#160; Went with the Nginx option.&#160; Mono comes with xsp, which is useful for local testing.

### Running a simple web application

To run xsp&#160; /usr/bin/xsp &#8211;port 9090 &#8211;root&#160; <path to your application>, and the application will be available on <http://localhost:9090>

&#160;

To install Nginx on OSX,&#160; get <a href="http://mxcl.github.com/homebrew/" target="_blank">Homebrew</a>.&#160; And then simply&#160; _sudo brew install nginix_

Follow the instructions here <http://www.mono-project.com/FastCGI_Nginx> to configure Nginix to work with Mono’s FastCGI server.

On OSX, the Nginix configs can be found in /usr/local/etc/nginx/nginx.conf

This is the configuration I tried for my testing,

In /usr/local/etc/nginx/nginx.conf

server{   
&#160;&#160; listen 80;   
&#160;&#160; server_name localhost;   
&#160;&#160; access_log /<span class="kwrd">var</span>/log/nginx/localhost\_mono\_access.log;   
&#160;&#160; location / {   
&#160;&#160;&#160;&#160;&#160;&#160;&#160; root /Users/hibri/Projects/WebApp/;   
&#160;&#160;&#160;&#160;&#160;&#160;&#160; index <span class="kwrd">default</span>.aspx index.html;   
&#160;&#160;&#160;&#160;&#160;&#160;&#160; fastcgi_index <span class="kwrd">default</span>.aspx;   
&#160;&#160;&#160;&#160;&#160;&#160;&#160; fastcgi_pass 127.0.0.1:9000;   
&#160;&#160;&#160;&#160;&#160;&#160;&#160; include /usr/local/etc/nginx/fastcgi_params;   
&#160;&#160; }   
} 

Add the following lines to /usr/local/etc/nginx/fastcgi_params

<pre>fastcgi_param  PATH_INFO          "";
 fastcgi_param  SCRIPT_FILENAME    $document_root$fastcgi_script_name;</pre>

&#160;

Start Nginx.

Start the Mono FastCGI server

fastcgi-mono-server2
    
  
&#160;&#160;&#160;&#160; /applications=localhost:/:/Users/hibri/Projects/WebApp/ /socket=tcp:127.0.0.1:9000



And the application is available on <http://localhost>

### Web Frameworks

We use OpenRasta for the services I want to run on Linux. OR didn’t work out of the box. This is something I’ll be exploring in the next few days. 

Tried <a href="http://servicestack.net/" target="_blank">ServiceStack</a> too, and was able to get one our projects (<https://github.com/gregsochanik/basic-servicestack-catalogue>) working on Mono as is.&#160; <a href="https://github.com/NancyFx/Nancy" target="_blank">Nancy</a> is next on the list.