---
id: 447
title: The SSL Handshake
date: 2005-04-26T21:48:45+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2005/04/26/TheSSLHandshake.aspx
permalink: /2005/04/26/the-ssl-handshake/
categories:
  - .Net Web
---
From <http://support.microsoft.com/default.aspx?scid=kb;en-us;257591>


  


&nbsp;


  
<H2 class=subTitle><FONT size=2>SUMMARY</FONT></H2>
  
<DIV class=sbody>The Secure Sockets Layer (SSL) protocol uses a combination of public-key and symmetric-key encryption. Symmetric-key encryption is much faster than public-key encryption; however, public-key encryption provides better authentication techniques. An SSL session always begins with an exchange of messages called the SSL handshake. The handshake allows the server to authenticate itself to the client by using public-key techniques, and then allows the client and the server to cooperate in the creation of symmetric keys used for rapid encryption, decryption, and tamper detection during the session that follows. Optionally, the handshake also allows the client to authenticate itself to the server.
  
<DIV class=topOfPage>
  


<TABLE>
  <br /> <br /> 
  
  <TR>
    <br /> <TD class=image><A href="http://support.microsoft.com/default.aspx?scid=kb;en-us;257591#toc"><FONT size=2><IMG title="Back to the top" alt="Back to the top" src="http://support.microsoft.com/library/images/support/kbgraphics/public/en-us/upArrow.gif" /></FONT></A></TD><br /> <TD class=text><A href="http://support.microsoft.com/default.aspx?scid=kb;en-us;257591#toc"><FONT size=2>Back to the top</FONT></A></TD>
  </TR>
</TABLE></DIV></DIV><A id=kb2></A>


  
<H2 class=subTitle><FONT size=2>MORE INFORMATION</FONT></H2>
  
<DIV class=sbody>The steps involved in the SSL handshake are as follows (note that the following steps assume the use of the cipher suites listed in Cipher Suites with RSA Key Exchange: Triple DES, RC4, RC2, DES):
  
<TABLE class=list>
  

  



  
<TD class=number><FONT size=2>1.</FONT></TD>
  
<TD class=text><FONT size=2>The client sends the server the client&#8217;s SSL version number, cipher settings, session-specific data, and other information that the server needs to communicate with the client using SSL.</FONT></TD>
  



  
<TD class=number><FONT size=2>2.</FONT></TD>
  
<TD class=text><FONT size=2>The server sends the client the server&#8217;s SSL version number, cipher settings, session-specific data, and other information that the client needs to communicate with the server over SSL. The server also sends its own certificate, and if the client is requesting a server resource that requires client authentication, the server requests the client&#8217;s certificate.</FONT></TD>
  



  
<TD class=number><FONT size=2>3.</FONT></TD>
  
<TD class=text><FONT size=2>The client uses the information sent by the server to authenticate the server (see Server Authentication for details). If the server cannot be authenticated, the user is warned of the problem and informed that an encrypted and authenticated connection cannot be established. If the server can be successfully authenticated, the client proceeds to step 4.</FONT></TD>
  



  
<TD class=number><FONT size=2>4.</FONT></TD>
  
<TD class=text><FONT size=2>Using all data generated in the handshake thus far, the client (with the cooperation of the server, depending on the cipher being used) creates the pre-master secret for the session, encrypts it with the server&#8217;s public key (obtained from the server&#8217;s certificate, sent in step 2), and then sends the encrypted pre-master secret to the server. </FONT></TD>
  



  
<TD class=number><FONT size=2>5.</FONT></TD>
  
<TD class=text><FONT size=2>If the server has requested client authentication (an optional step in the handshake), the client also signs another piece of data that is unique to this handshake and known by both the client and server. In this case, the client sends both the signed data and the client&#8217;s own certificate to the server along with the encrypted pre-master secret. </FONT></TD>
  



  
<TD class=number><FONT size=2>6.</FONT></TD>
  
<TD class=text><FONT size=2>If the server has requested client authentication, the server attempts to authenticate the client (see Client Authentication for details). If the client cannot be authenticated, the session ends. If the client can be successfully authenticated, the server uses its private key to decrypt the pre-master secret, and then performs a series of steps (which the client also performs, starting from the same pre-master secret) to generate the master secret. </FONT></TD>
  



  
<TD class=number><FONT size=2>7.</FONT></TD>
  
<TD class=text><FONT size=2>Both the client and the server use the master secret to generate the session keys, which are symmetric keys used to encrypt and decrypt information exchanged during the SSL session and to verify its integrity (that is, to detect any changes in the data between the time it was sent and the time it is received over the SSL connection).</FONT></TD>
  



  
<TD class=number><FONT size=2>8.</FONT></TD>
  
<TD class=text><FONT size=2>The client sends a message to the server informing it that future messages from the client will be encrypted with the session key. It then sends a separate (encrypted) message indicating that the client portion of the handshake is finished. </FONT></TD>
  



  
<TD class=number><FONT size=2>9.</FONT></TD>
  
<TD class=text><FONT size=2>The server sends a message to the client informing it that future messages from the server will be encrypted with the session key. It then sends a separate (encrypted) message indicating that the server portion of the handshake is finished. </FONT></TD>
  



  
<TD class=number><FONT size=2>10.</FONT></TD>
  
<TD class=text><FONT size=2>The SSL handshake is now complete and the session begins. The client and the server use the session keys to encrypt and decrypt the data they send to each other and to validate its integrity.</FONT></TD>
  



  
<TD class=number><FONT size=2>11.</FONT></TD>
  
<TD class=text><FONT size=2>This is the normal operation condition of the secure channel. At any time, due to internal or external stimulus (either automation or user intervention), either side may renegotiate the connection, in which case, the process repeats itself.</FONT></TD></TABLE></DIV>