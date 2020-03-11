---
id: 369
title: 'RaspberryPi Setup &#8211; Miscellaneous Notes'
date: 2012-08-24T21:18:49+00:00
author: Greg Woods
layout: single
classes: wide
guid: http://gregwoods.co.uk/?p=369
permalink: /2012/08/raspberrypi-setup-miscellaneous-notes/
categories:
  - Linux
  - RaspberryPi
---
For basic setup, see [http://gregwoods.co.uk/2012/08/setting-up-the-raspberry-pi-the-basics/](http://gregwoods.co.uk/2012/08/setting-up-the-raspberry-pi-the-basics/ "http://gregwoods.co.uk/2012/08/setting-up-the-raspberry-pi-the-basics/")

## 

## Remote Access &#8211; Graphical

<pre><strong id="internal-source-marker_0.667615579906851"> </strong>sudo apt-get install xrdp</pre>

The remote desktop to that IP address. Full LXDE desktop shown, even though ‘startx’ was never run on the Pi itself. The remote desktop operates at the resolution of the connecting computer.

## Screen Resolution and other stuff

<a title="http://elinux.org/RPi_config.txt" href="http://elinux.org/RPi_config.txt" target="_blank">http://elinux.org/RPi_config.txt</a>

## Remote Access &#8211; SSH

already enabled in Wheezy

## Console Font Sizes

<pre>sudo dpkg-reconfigure console-setup
sudo reboot</pre>