---
id: 350
title: Upgrading the SSD on an old Eee PC 901
date: 2012-08-24T18:54:56+00:00

layout: single

guid: http://gregwoods.co.uk/?p=350
permalink: /2012/08/upgrading-the-ssd-on-an-old-eee-pc-901/
categories:
  - Linux
  - SysAdmin
---
## Problem

The Eee PC 901 XP edition comes with a 4Gb SSD for booting Windows, and a slower 8Gb one for storage. To reinstall XP Home with SP3, you will need more than 4Gb unless you want to spend weeks of your life trimming down a custom "XP Lite" installation disc.

The 8Gb disc is not installed to be easy to access. I read somewhere it is even soldered onto the motherboard, so replacing this is a no-go.

The 4Gb is easily accessible under the "maintenance" cover on the back of the netbook, so this is the solution. A 70mm long SSD was purchased to enable me to screw the card down.

Once installed, due to the way the Eee PC's hard disk interfaces are designed, the new SSD is recognised as a Primary Slave. This has 2 negative effects:  
1) You 8Gb secondary SSD now "disappears" from the BIOS, and cannot be used. I can live with this.  
2) At every boot, you are interuppted with a message to the effect of "Primary Master not found, Press F1 to continue" - this is a pain in the backside.

## Fixing it

Reading around, it turns out you can enable a feature in the BIOS called Boot Booster. This gets around the HiIt F1 error, and does make bootup a lot faster. Before the option even appears in the BIOS, you need to set up an EFI partition. Below are the steps to do this.

  * Boot GParted, shrink your Windows XP installation partition so that have at least 8Mb free at the end of the disk. I ended up with 39Mb
  * Make this parition 'Primary' and unformatted.
  * Note the location of the partition. Mine was /dev/sda2 (disk: /dev/sda. partition: 2)
  * Still in gParted, open a Terminal window 
      * sudo sfdisk -change-id /dev/sda 2 [note the space before the '2']
  * check it worked... 
      * sudo sfdisk -print-id /dev/sda 2
  * Reboot, press F2 to access BIOS

You should now have a Boot Booster option available

## References

[http://forum.eeeuser.com/index/php?/topic/24064-boot-booster-and-sda4-efi-partition/page\_\_st\_\_20](http://forum.eeeuser.com/index/php?/topic/24064-boot-booster-and-sda4-efi-partition/page__st__20 "http://forum.eeeuser.com/index/php?/topic/24064-boot-booster-and-sda4-efi-partition/page__st__20")