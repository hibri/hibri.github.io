---
id: 315
title: 'How to : Sign XML messages with a SHA-1 signature, for Adobe Content Server'
date: 2010-02-14T11:38:53+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2010/02/14/HowToSignXMLMessagesWithASHA1SignatureForAdobeContentServer.aspx
permalink: /2010/02/14/how-to-sign-xml-messages-with-a-sha-1-signature-for-adobe-content-server/
categories:
  - .Net General
---
The past week I’ve been doing a spike to talk to <a href="http://www.adobe.com/products/contentserver/" target="_blank">Adobe Content Server 4</a> (ACS4). Querying the content in ACS4 is done in a REST style. The client sends a XML message via HTTP POST to the admin endpoint. The endpoint details are in the documentation but are vague.&#160; This is usually at&#160; **<http://youracs4server/admin/EndPoint>**. 

These need a signed XML message, in the POST body. A typical message looks like this

<pre class="csharpcode"><span class="kwrd">&lt;</span><span class="html">request</span><span class="kwrd">&gt;</span>
    <span class="kwrd">&lt;</span><span class="html">nonce</span><span class="kwrd">&gt;</span>ABCD123==<span class="kwrd">&lt;/</span><span class="html">nonce</span><span class="kwrd">&gt;</span>
    <span class="kwrd">&lt;</span><span class="html">hmac</span><span class="kwrd">&gt;</span>XXXXXXXXX===<span class="kwrd">&lt;/</span><span class="html">hmac</span><span class="kwrd">&gt;</span>
    <span class="kwrd">&lt;</span><span class="html">distributor</span><span class="kwrd">&gt;</span>uid:8888-43434-34343434<span class="kwrd">&lt;/</span><span class="html">distributor</span><span class="kwrd">&gt;</span>
   <span class="kwrd">&lt;</span><span class="html">resource</span><span class="kwrd">&gt;</span>
     ......
   <span class="kwrd">&lt;/</span><span class="html">resouce</span><span class="kwrd">&gt;</span>
<span class="kwrd">&lt;/</span><span class="html">request</span><span class="kwrd">&gt;</span></pre>

<pre class="csharpcode"><span class="kwrd"></span></pre>

The hmac element contains the SHA1 signature&#160; of the XML message. The signature is generated using a shared secret.&#160; The signature is for the whole XML except the hmac element. Before signing the message, we have to construct the XML without the hmac, then sign it, and then add then hmac.

I did this by using a two stage Xml serialization process. This may not be the best way to do it, and there has to be a better solution.&#160; I created a class named SignedXMLSerializer, and this inherits from <a href="http://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx" target="_blank">XmlSerializer</a>. SignedXMLSerializer serializes objects that are of the base type Signable. The Signable class has two properties, Nonce and Hmac. Any class that has to be sent as a signed XML message must inherit from Signable

<pre class="csharpcode"><span class="kwrd">public</span> <span class="kwrd">abstract</span> <span class="kwrd">class</span> Signable
    {
        [XmlElement(<span class="str">"nonce"</span>)]
        <span class="kwrd">public</span> <span class="kwrd">string</span> Nonce { get; set; }

        [XmlElement(<span class="str">"hmac"</span>)]
        <span class="kwrd">public</span> <span class="kwrd">string</span> HMAC { get; set; }
    }</pre>



In the serialize method of the SignedXMLSerializer, we first generate the nonce. The nonce makes each message unique. Then we serialize the object to a string. The signature is generated using this string, and assigned it to the Hmac property.

We then serialize the signed object to the writer that was passed in.

<pre class="csharpcode"><span class="kwrd">public</span> <span class="kwrd">void</span> Serialize(T o, XmlTextWriter writer) {
            o.Nonce = GenerateNonce();
            StringBuilder stringBuilder = GetXMLToSign(o);
            <span class="kwrd">string</span> hmac = GetSignature(stringBuilder);
            o.HMAC = hmac;
            Serialize(writer, o);
        }</pre>

<pre class="csharpcode">To use the SignedXMLSerializer, pass in one of the <a href="http://msdn.microsoft.com/en-us/library/system.security.cryptography.hashalgorithm.aspx" target="_blank">HashAlgorithm</a> types. I’ve used SHA1 in my case.</pre>

<pre class="csharpcode">This makes it easier to use with different signing algorithms. </pre>

<pre class="csharpcode">Typical usage of the SignedXMLSerializer is as follows</pre>

<pre class="csharpcode">HMACSHA1 hmacsha1 = <span class="kwrd">new</span> HMACSHA1 {Key = Encoding.ASCII.GetBytes(<span class="str">"consumerSecret"</span>)};
            SignedXmlSerializer&lt;Request&gt; signedXmlSerializer = <span class="kwrd">new</span> SignedXmlSerializer&lt;Request&gt;(hmacsha1);

 StringBuilder sb = <span class="kwrd">new</span> StringBuilder();
            StringWriter writer = <span class="kwrd">new</span> StringWriter(sb);
            signedXmlSerializer.Serialize(req, <span class="kwrd">new</span> XmlTextWriter(writer));</pre>

The final serialized string can be sent via HTTP post to ACS4.&#160; 

Code for the SignedXMLSerializer class is here [http://gist.github.com/303962](http://gist.github.com/303962 "http://gist.github.com/303962")

<div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:dce654d7-c3f9-4b00-8118-1e8524af3791" class="wlWriterEditableSmartContent">
  del.icio.us Tags: <a href="http://del.icio.us/popular/%22Adobe+Content+Server%22" rel="tag">"Adobe Content Server"</a>,<a href="http://del.icio.us/popular/xml" rel="tag">xml</a>,<a href="http://del.icio.us/popular/sha-1" rel="tag">sha-1</a>,<a href="http://del.icio.us/popular/%22signing+xml+messages%22" rel="tag">"signing xml messages"</a>
</div>