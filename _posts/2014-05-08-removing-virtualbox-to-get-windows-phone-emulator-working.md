---
id: 474
title: Removing VirtualBox to get Windows Phone Emulator Working
date: 2014-05-08T10:32:25+00:00
author: Greg Woods
layout: single
classes: wide
guid: http://gregwoods.co.uk/?p=474
permalink: /2014/05/removing-virtualbox-to-get-windows-phone-emulator-working/
categories: programming sysadmin
---
I always preferred VirtualBox&#8217;s simplicity over the Enterprise class complexity of Windows 8 Hyper-V.  
However, in order to get a working Windows Phone 8 Emulator working, you need to use Hyper-V.  
Unfortunately when trying to do this, I got an error saying that the virtual switch could not be created. I tried some fixes from <a href="http://stackoverflow.com/questions/13149509/windows-phone-8-emulator-error-something-happened-while-creating-a-switch" title="StackOverflow Question" target="_blank">StackOverflow</a> and <a href="http://superuser.com/questions/247392/unable-to-uninstall-virtualbox-network-drivers" title="superuser question" target="_blank">ServerFault</a>, but they didn&#8217;t work. I couldn&#8217;t create nay kind of virtual switch in Hyper-V. A common theme from my searching was that VirtualBox was involved.

Uninstalling VirtualBox manually didn&#8217;t help.  
Looking in the registry, I noticed hundreds of network adapters with a VirtualBox driver (just search the registry for &#8216;vbox&#8217;)  
I couldn&#8217;t delete these keys even with Admin privileges  
Apparently I needed to run Regedit as &#8216;System&#8217;  
THe easiest way to do this was using <a href="http://live.sysinternals.com/" title="sysinternals live" target="_blank">SysInternals Psexec</a>

`C:\Windows\System32\> psexec /i /s regedit`

/i means &#8216;interactive&#8217;, or allow the program to display a UI  
/s means run the program as the &#8216;system&#8217; user

Because there were so many to delete, it was easier to export the parent key, edit in Notepad, then save as a .reg file and re-import.

After doing this, removing all references to &#8216;vbox&#8217; and &#8216;virtualbox&#8217; from the registry, deleting other invisible network adapters from the registry, running cccleaner, rebooting, removing Hyper-V from Windows, rebooting again, Adding Hyper-V to windows&#8230; I finally got my emulator to work.

Lesson: Don&#8217;t ever install VirtualBox, stick to Hyper-V (as long as you meet Microsoft&#8217;s <a href="http://social.technet.microsoft.com/wiki/contents/articles/1401.hyper-v-list-of-slat-capable-cpus-for-hosts.aspx" title="Hyper-V hardware requirements" target="_blank">bizarrely restrictive processor requirements</a> of course)