---
id: 375
title: Adding simple authentication to a web service using SOAP headers
date: 2006-11-26T11:59:53+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2006/11/26/AddingSimpleAuthenticationToAWebServiceUsingSOAPHeaders.aspx
permalink: /2006/11/26/adding-simple-authentication-to-a-web-service-using-soap-headers/
categories:
  - .Net Web
---
If you ever wanted to add a simple username/password authentication to your web service, but ended up with a whole lot of this ?

[WebMethod]  
public string HelloWorld(string userName,string password)

Well then, here is a much cleaner way. You can use SOAP headers to pass extra information to a web service. This method uses SOAP headers to pass the user credentials to the web service.

**The web service.**

We need an object to hold the user credentials. For this example a simple class with username and password properties would suffice. The class should derive from the SoapHeader class.

<pre><span style="color: blue">public</span> <span style="color: blue">class</span> Authentication:SoapHeader
{
    <span style="color: blue">private</span> <span style="color: blue">string</span> _userName;
    <span style="color: blue">private</span> <span style="color: blue">string</span> _password;
	
    <span style="color: blue">public</span> <span style="color: blue">string</span> Password
    {
        <span style="color: blue">get</span> { <span style="color: blue">return</span> _password; }
        <span style="color: blue">set</span> { _password = value; }
    }

    <span style="color: blue">public</span> <span style="color: blue">string</span> UserName
    {
        <span style="color: blue">get</span> { <span style="color: blue">return</span> _userName; }
        <span style="color: blue">set</span> { _userName = value; }
    }
}
</pre>

In the web service class, declare a public&nbsp;field (or property)&nbsp;of the Authentication type.

[WebService(Namespace = &#8220;[http://tempuri.org/&#8221;)]](http://tempuri.org/")])  
[WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1,Name=&#8221;MyWebService&#8221;)]  
<span style="color: blue">public</span> <span style="color: blue">class</span> MyWebService : System.Web.Services.WebService {  
&nbsp;&nbsp;&nbsp; <span style="color: blue">public</span> Authentication ServiceCredentials; 

In the next step, set up the web method to accept a SOAP header, of the type Authentication, and assign the value to the ServiceCredentials member.

<pre>[WebMethod]
    [SoapDocumentMethod(Binding=<span style="color: maroon">"MyWebService"</span>)]
    [SoapHeader(<span style="color: maroon">"ServiceCredentials"</span>) ]
    <span style="color: blue">public</span> <span style="color: blue">string</span> HelloWorld() {
        <span style="color: blue">if</span> (ServiceCredentials.UserName == <span style="color: maroon">"test"</span> && <br />                ServiceCredentials.Password == <span style="color: maroon">"world"</span>) {
            <span style="color: blue">return</span> <span style="color: maroon">"Hello World"</span>;
        }
        <span style="color: blue">else</span>
        {
            <span style="color: blue">return</span> <span style="color: maroon">"Invalid authentication"</span>;
        }
    }</pre>

**&nbsp;At the client.**

  1. Add the web service reference as usual. Instantiate a new object of the type MyWebService. 
      * In addition instantiate a new object of the type Authentication and assign the username and password properties. 
          * Next, assign this to the Service credentials property of the MyWebService instance. 
              * Call any web method, as you like. </ol> 
            The credentials are being passed with the soap headers, so you don&#8217;t need to add the username/password to each and every method. Since, this is done once for the web service, it can be used for multiple calls to any web method in the same service.
            
            This is how the SOAP XML looks like,
            
            
<font face="Courier New"> 
            
            <pre><span style="color: blue">&lt;?</span><span style="color: maroon">xml</span> <span style="color: red">version</span>="<span style="color: blue">1.0</span>" <span style="color: red">encoding</span>="<span style="color: blue">utf-8</span>"<span style="color: blue">?&gt;</span>
<span style="color: blue">&lt;</span><span style="color: maroon">soap:Envelope</span> <span style="color: red">xmlns:xsi</span>="<span style="color: blue">http://www.w3.org/2001/XMLSchema-instance</span>" <br /><span style="color: red">xmlns:xsd</span>="<span style="color: blue">http://www.w3.org/2001/XMLSchema</span>" <br /><span style="color: red">xmlns:soap</span>="<span style="color: blue">http://schemas.xmlsoap.org/soap/envelope/</span>"<span style="color: blue">&gt;</span>
  <span style="color: blue">&lt;</span><span style="color: maroon">soap:Header</span><span style="color: blue">&gt;</span>
    <span style="color: blue">&lt;</span><span style="color: maroon">Authentication</span> <span style="color: red">xmlns</span>="<span style="color: blue">http://tempuri.org/</span>"<span style="color: blue">&gt;</span>
      <span style="color: blue">&lt;</span><span style="color: maroon">Password</span><span style="color: blue">&gt;</span>string<span style="color: blue">&lt;</span>/<span style="color: maroon">Password</span><span style="color: blue">&gt;</span>
      <span style="color: blue">&lt;</span><span style="color: maroon">UserName</span><span style="color: blue">&gt;</span>string<span style="color: blue">&lt;</span>/<span style="color: maroon">UserName</span><span style="color: blue">&gt;</span>
    <span style="color: blue">&lt;</span>/<span style="color: maroon">Authentication</span><span style="color: blue">&gt;</span>
  <span style="color: blue">&lt;</span>/<span style="color: maroon">soap:Header</span><span style="color: blue">&gt;</span>
  <span style="color: blue">&lt;</span><span style="color: maroon">soap:Body</span><span style="color: blue">&gt;</span>
    <span style="color: blue">&lt;</span><span style="color: maroon">HelloWorld</span> <span style="color: red">xmlns</span>="<span style="color: blue">http://tempuri.org/</span>" /<span style="color: blue">&gt;</span>
  <span style="color: blue">&lt;</span>/<span style="color: maroon">soap:Body</span><span style="color: blue">&gt;</span>
<span style="color: blue">&lt;</span>/<span style="color: maroon">soap:Envelope</span><span style="color: blue">&gt;</span></pre>
            
            <p>
              </font>
            </p>