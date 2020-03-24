---
id: 359
title: 'Setting up the Raspberry Pi - the basics'
date: 2012-08-24T21:00:58+00:00

layout: single

guid: http://gregwoods.co.uk/?p=359
permalink: /2012/08/setting-up-the-raspberry-pi-the-basics/
categories:
  - Linux
  - RaspberryPi
---
## First Steps

  * Download the Wheezy Raspian distribution, along with Win32DiskImager.exe (Assuming you’re on Windows)  from <a title=" http://www.raspberrypi.org/downloads" href=" http://www.raspberrypi.org/downloads" target="_blank">http://www.raspberrypi.org/downloads</a>
  * Write the image to the SD card, pop it into the Raspberry Pi, and connect it to you network.
  * Don’t power up until you’ve changed some settings on your DHCP server (usually this means your broadband router)
  * You’ll also need an SSH Telnet client. Putty is pretty universal for windows.

## Setting up without need for the TV (Headless)

SSH is enabled by default in Wheezy, which is extremely useful compared to the previous distro. I recommend you reserve a DHCP IP address for your Raspberry Pi in your DHCP Server / Router configuration. This saves the hassle of changing the Raspberry Pi to a fixed IP address. Feel free to upvote my answer at http://raspberrypi.stackexchange.com/questions/1409/easiest-way-to-show-my-ip-address/1481#1481

### Reserve an IP address on the Router

Your router should allow linking the Pi’s network adapter’s MAC address with a reserved IP address.  
Power up the Pi and look in your router connections page to get the MAC address of the device you don’t recognise (this will be the Raspberry Pi)  
I reserved 192.168.0.100 for the MAC starting B8:27:*

### Or Set a Fixed IP address

find the IP address your Pi has obtained from the DHCP server. Your broadband router should have a page which shows connected clients and their IP addresses.

Connect to the Pi using Putty (SSH client), with the IP address you obtained.

<pre>sudo nano /etc/network/interfaces</pre>

replace

<pre>iface etho0 inet dhcp</pre>

with... (adjust to your environment, obviously)

<pre>iface eth0 inet static
 address 192.168.0.3
 netmask 255.255.255.0
 gateway 192.168.0.2</pre>

&nbsp;

## Basic Linux Configuration

If you have Wheezy installed, and you can SSH into a shell prompt, you’re good to go.

Discaimer: I’m not a Linux geek, so helpful suggestions are welcome, but please be kind!

#### Password Change

default username/password: pi/raspberry

<pre>passwd</pre>

#### Get Updates

takes several minutes

<pre>sudo apt-get update && sudo apt-get upgrade</pre>

#### Misc Config

(not entirely sure what the upgrade raspi config does)

<pre>sudo raspi-config</pre>

expand_rootfs  
set timezone (or it defaults to UST instead of BST) (NTP is set up on Debian)  
upgrade raspi config

<pre>sudo reboot</pre>

#### Take a Backup

<pre>sudo shutdown -h now</pre>

Use Win32DiskImager to backup the whole 4Gb SD card - though the process is faster if you do it before resizing the partition!