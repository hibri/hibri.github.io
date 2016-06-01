---
id: 402
title: Use iTunes to manage MP3s on your W800i Walkman phone
date: 2006-01-01T10:51:49+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2006/01/01/UseITunesToManageMP3sOnYourW800iWalkmanPhone.aspx
permalink: /2006/01/01/use-itunes-to-manage-mp3s-on-your-w800i-walkman-phone/
categories:
  - .Net UI
  - iPod
  - w800i iTunes Syncher
---
The problem with Sony MP3 players is that the software is not intuitive and
  
buggy. The Disc2Phone application included with&nbsp;my Sony Ericsson W800i
  
fails to copy audio tracks to the phone properly. I was looking for a way to use
  
Winamp or iTunes to manage the MP3s on the phone. As it turned out, I was able
  
to do it with iTunes.&nbsp; 

I was able to wrap it all up in a small C# program. Download it from [here](/content/binary/synchsetup.msi)&nbsp;. Update : this now also
  
deletes files on the phone that are not in the play list, keeping it completely
  
in sync. It only deletes files inside the MP3 directory, so dont put anything
  
else in there 🙂

**Instructions:**  
1. Install all of the requirements.  
2.
  
[Download the setup](/content/binary/synchsetup.msi) and
  
install.  
3. Start iTunes, if it is not started the program will start it for
  
you, but be patient.  
4. Select the playlist you want to synch with the phone.
  
It is better to create a new playlist like &#8220;W800i List&#8221; and add your tracks to
  
this.  
5. Click on the **Synch** button to start
  
synchronising.  
6. This takes a while. You can speed up the copy process by
  
using a Memory Stick reader, which is faster than going through the USB data
  
cable. Take the memory stick out of the phone, put it in the reader, plug the
  
reader in and synch.

Disclaimer: Use the program at your own risk. This program is un-supported
  
and I will not be held for any damages, liabilities, warranties, natural
  
disasters and if your dog eats it. However, feel free to report bugs and
  
features.

**Requirements:**

[.Net
  
2.0 Framework](http://www.microsoft.com/downloads/details.aspx?FamilyID=0856EACB-4362-4B0D-8EDD-AAB15C5E04F5&displaylang=en)  
[iTunes 6.0](http://www.apple.com/itunes) 

**How it all works**

When plugged in to the computer,the phone is bacially a Mass Storage Device
  
just like any other USB flash drive. The Memory Stick on the phone contains a
  
directory &#8220;MP3&#8221;. All that needs to be done is to copy the MP3s to this folder.
  
Use the&nbsp;**[System.IO.DriveInfo.GetDrives()](http://msdn2.microsoft.com/en-us/library/0fxtk2z5(en-US,VS.80).aspx)**
  
method of the **[DriveInfo](http://msdn2.microsoft.com/en-us/library/abt1306t(en-US,VS.80).aspx)**&nbsp;class
  
in .Net 2.0&nbsp; to get an array of DriveInfo objects representing all the
  
drives on the computer. Iterate through this array to check for removable drives
  
using the **DriveInfo.DriveType** property and then check for
  
drives that have a &#8220;MP3&#8221; directory in the root. Use the
  
**DriveInfo.IsReady** to check if the removable disc is ready.

The next step is to copy only the MP3s in a specific iTunes playlist. iTunes
  
has an exellent COM interface. To program against this in C#, add a COM
  
reference to the **&#8220;iTunes 1.6 Type Library&#8221;**. iTunes is started
  
by;

<font size="2"></p> 

<p>
  itunesApp = </font><font color="#0000ff" size="2">new</font><font size="2"><br /> </font><font color="#008080" size="2">iTunesAppClass</font><font size="2">(); </p> 
  
  <p>
    </font>
  </p>
  
  <p>
    Use the iTunesAppClass to get the collection of playlists;
  </p>
  
  <p>
    <font size="2"></p> 
    
    <p>
      playlistCollection = itunesApp.LibrarySource.Playlists;
    </p>
    
    <p>
      </font>
    </p>
    
    <p>
      You can then get a specific playlist, like the playlist you want to synch the<br /> phone with;
    </p>
    
    <p>
      <font size="2"></p> 
      
      <p>
        playListToSynch = playlistCollection.get_ItemByName(&#8220;W800i&#8221;);
      </p>
      
      <p>
        </font>
      </p>
      
      <p>
        The playlist will have a collection of&nbsp;<font color="#008080" size="2">IITFileOrCDTrack</font>&nbsp;objects. Each&nbsp;<font color="#008080" size="2">IITFileOrCDTrack</font>&nbsp;object has&nbsp; Artist,Album and Location<br /> properties. The Location property gives the physical location of the audio track<br /> on the computer. This is used to copy the track to the phone. Iterate through<br /> the tracks in the playlist and copy the files to the phone. Thats all there is<br /> to it. With this technique it is possible to use iTunes with other USB type<br /> devices that play MP3&#8217;s.
      </p>
      
      <p>
        <strike>The next step is to improve the synch functionality, right now it is<br /> just a one way copy process.</strike> Update : This functionality is now<br /> included.<font color="#008080" size="2">&nbsp;</p> 
        
        <p>
          <p>
            &nbsp;
          </p>
          
          <p>
            </font>
          </p>