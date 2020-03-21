---
id: 49
title: Creating a WinPE Boot DVD for Disk Cloning
date: 2010-04-23T16:55:31+00:00
author: Greg Woods
excerpt: |
  <p>I recently had to rebuild my PC at work. Knowing that this takes about a week to get fully up to speed, I thought it’d be useful to image the disk once I’d got all the apps installed, so that other devs can quickly get up and running. The last time I did this was 2008 using Vista, and unfortunately, I’d lost the WinPE (Preinstall Environment) boot disk required to do the cloning.</p>
  
  <p>The process has changed in Windows 7, so here’s the steps I took to create a Windows 7 working WinPE boot disk. </p>
layout: single
classes: wide
guid: http://gregwoods.co.uk/?p=49
permalink: /2010/04/creating-a-winpe-boot-dvd-for-disk-cloning/
categories:
  - SysAdmin
---
**UPDATED September 2010:** Added section on adding custom drivers

A custom Windows PE boot disc can be used to boot quickly to a windows command prompt, complete with additional drivers already loaded. These drivers could be for an exotic hard disk controller, or unusual network adapter. I have used this at work to allow network deployment of a customised windows image file. 

Below are the steps I took to get a useful WinPE boot disc (command prompt only).

  * Install the The [Windows® Automated Installation Kit (AIK) for Windows® 7](http://www.microsoft.com/downloads/details.aspx?familyid=696DD665-9F76-4177-A811-39C26D3B3B34&displaylang=en)
  * Open a WAIK elevated command prompt
  * copype.cmd amd64 d:\win7pe
  * `copy d:\win7pe\winpe.wim d:\win7pe\ISO\sources\boot.wim`
  * `Dism /Mount-Wim /WimFile:D:\win7pe\ISO\sources\boot.wim /index:1 /MountDir:D:\win7pe\mount`
  * Copy ImageX to the mounted iso image (crazy that it's not included) 
      * `copy "C:\Program Files\Windows AIK\Tools\amd64\imagex.exe" D:\win7pe\mount\Windows\System32`
  * Copy BootRec to the mounted iso image (the util that allows easy boot problem repairs). We must get this util by mounting a Windows 7 DVD and extracting the relevant files. 
      * `copy <windvd>\sources\boot.wim d:\win7dvd.wim`
      * `Dism /Mount-Wim /WimFile:d:\win7dvd.wim /index:1 /MountDir:D:\win7dvd\mount`
      * `copy d:\win7dvd\mount\windows\system32\Bootrec.exe d:\win7pe\mount\windows\system32`
      * `copy d:\win7dvd\mount\windows\system32\wer.dll d:\win7pe\mount\windows\system32`
      * `copy d:\win7dvd\mount\windows\system32\en-US\Bootrec.exe.mui d:\win7pe\mount\windows\system32\en-US`
      * `copy d:\win7dvd\mount\windows\system32\en-US\wer.dll.mui d:\win7pe\mount\windows\system32\en-US`
      * `Dism /unmount-Wim /MountDir:D:\win7dvd\mount /discard`
  * Add drivers (used this step to make the boot disc compatible with the Lenovo laptops) 
      * Downloaded a Dell driver package CAB file (various sources say it includes the drivers used by the Lenovo range) [Dell driver bundle](http://support.dell.com/support/downloads/download.aspx?c=us&cs=04&l=en&s=gen&catid=-1&dateid=-1&deviceid=22327&devlib=0&fileid=360733&formatcnt=0&formatid=-1&impid=-1&libid=36&os=WLH&osl=en&releaseid=R247360&servicetag=&SystemID=LAT_E6400&typecnt=0&typeid=-1&vercnt=2)
      * Extracted the CAB file using 7zip to D:\drivers
      * `Dism /image:D:\win7pe\mount /Add-Driver /driver:D:\drivers\winpe\x64 /recurse`
  * close any folders pointing to D:\win7pe\mount, or the commit will fail
  * `Dism /unmount-Wim /MountDir:D:\win7pe\mount /Commit`
  * `oscdimg n bD:\win7pe\etfsboot.com D:\win7pe\ISO D:\win7pe\win7pe_amd64_bootdisk.iso`
  * Burn d:\win7pe\win7pe\_amd64\_bootdisk.iso to DVD using your favourite tool
  * Copy the ISO for later use, to \\server\share\foldername