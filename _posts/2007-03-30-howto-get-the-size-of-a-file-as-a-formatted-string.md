---
id: 363
title: HOWTO Get the size of a file as a formatted string
date: 2007-03-30T13:54:54+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2007/03/30/HOWTOGetTheSizeOfAFileAsAFormattedString.aspx
permalink: /2007/03/30/howto-get-the-size-of-a-file-as-a-formatted-string/
categories:
  - .Net General
---
Quick and dirty function to return the size of a file in a properly formatted string in KB, MB or GB. There has to be an easier way than this &#8230;..

&nbsp;

<pre><span style="color: blue">private</span> <span style="color: blue">const</span> <span style="color: blue">double</span> KByte = <span style="color: maroon">1024</span>;
    <span style="color: blue">private</span> <span style="color: blue">const</span> <span style="color: blue">double</span> MByte = KByte * <span style="color: maroon">1024</span>;
    <span style="color: blue">private</span> <span style="color: blue">const</span> <span style="color: blue">double</span> GByte = MByte * <span style="color: maroon">1024</span>;

<span style="color: blue">public</span> <span style="color: blue">static</span> <span style="color: blue">string</span> GetFileSizeString(<span style="color: blue">int</span> bytes) {
        <span style="color: blue">if</span> ((bytes / GByte) &lt; <span style="color: maroon">1</span>) {
            <span style="color: blue">if</span> ((bytes / MByte) &lt; <span style="color: maroon">1</span>) {
                <span style="color: blue">if</span> ((bytes / KByte) &lt; <span style="color: maroon">1</span>) {
                    <span style="color: blue">return</span> String.Format(<span style="color: maroon">"{0} B"</span>, bytes);
                }
                <span style="color: blue">else</span> {
                    <span style="color: blue">return</span> String.Format(<span style="color: maroon">"{0} KB"</span>, Math.Round((bytes / KByte), <span style="color: maroon">2</span>));
                }
            }
            <span style="color: blue">else</span> {
                <span style="color: blue">return</span> String.Format(<span style="color: maroon">"{0} MB"</span>, Math.Round((bytes / MByte), <span style="color: maroon">2</span>));
            }
        }
        <span style="color: blue">else</span> {
            <span style="color: blue">return</span> String.Format(<span style="color: maroon">"{0} GB"</span>, Math.Round((bytes / GByte), <span style="color: maroon">2</span>));
        }
        
    }</pre>