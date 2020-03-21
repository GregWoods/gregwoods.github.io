---
id: 377
title: Windows 8 Pro Upgrade for £25 with Just a Vista COA
date: 2012-11-28T01:48:42+00:00
author: Greg Woods
layout: single
classes: wide
guid: http://gregwoods.co.uk/?p=377
permalink: /2012/11/dodgy-way-to-get-my-legitimate-windows-8-upgrade/
categories:
  - SysAdmin
---
My secondhand laptop was supplied with Windows Vista Home Premium - though I've always run it with an MSDN copy of Windows 7, and more recently Windows 8. However, after reading carefully the small print of the licence agreement, it turns out that I wasn't completely legal in doing this. You have to be using the PC exclusively for software development to be legit... as far as I can tell.

So, when I saw the opportunity to upgrade my legitimate Windows Vista Home Premium to Windows 8 Pro, for the princely sum of £24.99, I had to go for it.

The problem is that in order to get to my download (which I don't really need), and the Product Key (which I do need), is the Upgrade Assistant. This app checks that the operating system you are running qualifies for the upgrade. My problem is that I'm already running Win8, and don't want to wipe it, then install Vista, then have to upgrade it to Win8 again. I tried the process using a virtual machine, but I still needed a Vista OEM disc, but I  don't have one, as Acer preloaded the OS onto the hard disk.

Here's my slightly "irregular" solution

  * Download a Vista Home Premium torrent (told you it was irregular) - Unfortunately, unadulterated iso files are hard to find, the ones with activation "workarounds" are well seeded, so I got one of those.
  * Create a new Virtual Box VM, with 1024Mb RAM (any less and the upgrade advisor fails)
  * Mount the Vista  iso on the VM, Install Vista
  * When prmoted, use the genuine Product Key from the Certificate of Authenticity stuck to the PC
  * The online activation appears to have been crippled on this iso - you are supposed to use a very naughty program included on the iso to trick the OS into believing it is activated. Do NOT use this, you need to be genuinely activated to proceed
  * Search for 'Activation' in the Vista Start Menu, and launch the wizard
  * Although the online activation is crippled, you can still be able to use the Automated Telephone Activation service. You dial a freephone number, type in some numbers, get some numbers back, enter them into the wizard. Hey presto, activated legitimately.
  * Run the Windows  8 Upgrade Assistant, pass all the checks, hand over your credit card details
  * Start the download and get a shiny new Product Key
  * Now to apply the new licence key to my already installed Win8 Pro (MSDN Subscriber) 
      * Open an elevated command prompt, type (with your new product key)
      * slmgr.vbs /ipk 12345-12345-12345-12345-12345
      * Win8 will activate automatically
  * Job done, the VM can be deleted
  * Even though I had no need for the upgrade download, it's still wise to save it. You get an option to save an iso or save to USB disk.

The downloaded file appears not to care about whether you are upgrading or performing a fresh install. I tested a new instalation on another new VM, and the installation process proceeded up to the entering Product Key dialog without complaining about there being no qualifying OS present. This is good news. I didn't try  to input the product key obviously, as I had used it already, but I'm confident that if I had to perform a clean install on this laptop, I wouldn't have to go through the trauma of installing Windows Vista first.

I hope this info encourages more people to use those COA stickers to upgrade to Windows 8 for £25. Note: offer is "for a limited time" - which I'm sure I read somewhere is Jan 2013.