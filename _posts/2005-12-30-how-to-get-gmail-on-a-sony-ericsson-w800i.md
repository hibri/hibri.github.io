---
id: 403
title: How to get GMail on a Sony Ericsson W800i
date: 2005-12-30T18:23:18+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2005/12/30/HowToGetGMailOnASonyEricssonW800i.aspx
permalink: /2005/12/30/how-to-get-gmail-on-a-sony-ericsson-w800i/
categories:
  - 'Odds &amp; Sods'
---
This should apply for the K750i as well. The w800i&nbsp;phone has a built-in
  
POP email client. GMail uses SSL for both POP and SMTP e-mail transfers.&nbsp;
  
The w800i has support for SSL/TLS in its mail client. 

However, the phone does not come with two&nbsp;root
  
certificates&nbsp;required to get Gmail to work. Gmail uses two different
  
certificates on pop.gmail.com and smtp.gmail.com, and each of these certificates
  
are issued by two certification authorities. The trick to get gmail to work is
  
simply install the root certificates of these two CAs. These are Thawte and
  
Equifax.

To get the root certificates, open the Certificates manager in Windows XP or
  
2000 ( open a blank Microsoft Management Console , by typing mmc at the command
  
prompt, and then add the Certificates snap-in). In the certificates tree, under
  
Trusted Root Certification Authorities , find the certificate for Equifax Secure
  
Certification Authority and Thawte Premium Server CA. 

Now, export each of these certificates in turn as a DER encoded binary X.509
  
certificate. Send these two files via a bluetooth or infrared link (does not
  
work when the files are copied using file manager ). The phone will prompt to
  
accept the certificates&nbsp;and you are good to go :).

Gmail also has a mobile interface at <http://m.gmail.com>, but this is not good enough to
  
compose emails.