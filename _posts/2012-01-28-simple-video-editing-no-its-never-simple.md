---
id: 264
title: 'Simple Video Editing (No, it&#8217;s never simple)'
date: 2012-01-28T00:11:42+00:00
author: Greg Woods
layout: post
guid: http://gregwoods.co.uk/?p=264
permalink: /2012/01/simple-video-editing-no-its-never-simple/
categories:
  - VideoEditing
---
&nbsp;

I went snowboarding last week. I took along a £99 Samsung WM200 pocket camcorder. I didn&#8217;t take many clips, and they weren&#8217;t that good, but I knew they could be improved by shortening and splicing a couple together to form a short sequence. I&#8217;ve use Premiere Pro a little in the past, and although it did everything I wanted it to, nothing was ever intuitive (like most Adobe products). So I decided to suppress some of my creative urges and use the simplest app I could find, Windows Live Movie maker.

For the quick edit I had in mind, opened the Samsun W200 MP4 files, and worked well. But there&#8217;s always just one more tweak! This time it was the sound. The built in mic picked up a lot of background music outside the mountain restaurant where I&#8217;d interviewed one of my ski buddies. All I needed to do was put the sound through an equaliser to remove the bass, and boost the gain. Unfortunately, WLMM doesn&#8217;t have such an option. I&#8217;d need to extract the audio, tinker with it in a free audio editor, then re-add to my video project, hoping the lip-sync was still ok. The problem is that none of the many utilities I tried would open the MP4 file. Odd, since it played fine in Media Player, Zune, and Movie Maker. The application I really wanted to open it up in was VirtualDub. I don&#8217;t even know for sure that I can extract the audio using this awesome utility, but I&#8217;d be very surprised if it couldn&#8217;t be done somehow.

So the next part of my mission came to be opening the MP4 file in VirtualDub.

After installing lots of apps and codecs, and failing to make progress, I stumbles across this YouTube tutorial [youtube.com](http://www.youtube.com/watch?v=nXLEAScqN0U) , and followed the steps. For the sake of my own future sanity, I&#8217;ve noted them here.

  * Start fresh &#8211; uninstall as many codec and video editing apps you can find 
      * ffdshow
      * virtualDub
      * Quicktime
      * Codec packs
  * Install a fresh new copy of VirtualDub
  * Install the K-Lite Codec pack, both 32bit and 64bit versions (I have Win7 64bit) 
      * Leave the configuration until later
  * Install updated ffdshow MPEG-4 codec, both 32bit and 64bit version
  * Configure ffdshow (make sure H. 264/AVC is assigned a decoder)
  * Install AviSynth (this is the important bit)
  * For each video file you need to open in VirtualDub, create a .AVS script file 
      * In it, simply add the following line:
      * DirectShowSource(&#8220;fullPathAndFilename.mp4&#8243;)

At first I thought that creating this script file every clip was a bind. Then I glanced over the documentation [avisynth.org ](http://avisynth.org "avisynth.org")

You can script your video editing! As a programmer this is awesome. I could source control my edits. If I decide to swap editing software, I don&#8217;t have to start everything again, as my filter settings, in and out points, andf likely a ton of other stuff is safe in my text file.

I&#8217;ve yet to explore this properly &#8211; this is one evening&#8217;s exploration, so there should be more to come.

&nbsp;