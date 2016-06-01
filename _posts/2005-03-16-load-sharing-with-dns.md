---
id: 458
title: Load Sharing with DNS
date: 2005-03-16T17:46:21+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2005/03/16/LoadSharingWithDNS.aspx
permalink: /2005/03/16/load-sharing-with-dns/
categories:
  - High Availability
---

  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  I was looking at how to implement a load balancing/load sharing system for a data centre.<SPAN style="mso-spacerun: yes">&nbsp; </SPAN>The data centre hosts websites and other servers on a domain name www.mydomain.com&nbsp;(for example). Servers within the data centre are load balanced by Cisco Content Switches. The company wants 3 data centres. The traffic coming to www.mydomain.com should be shared among the data centres providing redundancy and scalability. These 3 data centres are in different physical locations, and will be served by different ISPs (ideally).
</P>


  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  &nbsp;
</P>


  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  The solution to this is to implement a DNS based load balancing system. In this solution the primary name server for www.mydomain.com will be replaced with an &#8220;intelligent&#8221; DNS server.
</P>


  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  Instead of replying to DNS request with just one IP address, this smart DNS server will give out the IP addresses based on the load at each of the data centres. The client resolving an IP address for www.mydomain.com will get the IP address of the data centre with the least load.
</P>


  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  The DNS server can also stop clients from going to a data centre that is not functioning.
</P>


  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  This solution is explained in more detail at <A href="http://ntrg.cs.tcd.ie/undergrad/4ba2.01/group8/DNS.html">http://ntrg.cs.tcd.ie/undergrad/4ba2.01/group8/DNS.html</A>
</P>


  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  &nbsp;
</P>


  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  These are some of the solutions available in the market.
</P>


  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  &nbsp;
</P>


  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  <A href="http://www.sysmaster.com/s_net_dns.htm">http://www.sysmaster.com/s_net_dns.htm</A>
</P>


  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  &nbsp;
</P>


  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  <A href="http://www.cisco.com/en/US/netsol/ns340/ns394/ns50/ns254/networking_solutions_white_paper09186a00801b7725.shtml">Cisco GSS Global Server Load-Balancing</A>
</P>


  


<P style="FONT-SIZE: 10pt; MARGIN: 0in; FONT-FAMILY: Verdana; mso-outline-level: 1">
  <A href="http://www.cisco.com/en/US/netsol/ns340/ns394/ns50/ns254/networking_solutions_white_paper09186a00801b7725.shtml"></A>&nbsp;
</P>