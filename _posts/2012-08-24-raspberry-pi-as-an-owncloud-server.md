---
id: 355
title: Raspberry Pi as an OwnCloud Server
date: 2012-08-24T21:14:51+00:00

layout: single
classes: wide
guid: http://gregwoods.co.uk/?p=355
permalink: /2012/08/raspberry-pi-as-an-owncloud-server/
categories:
  - Linux
  - RaspberryPi
---
First, see [http://gregwoods.co.uk/2012/08/setting-up-the-raspberry-pi-the-basics/](http://gregwoods.co.uk/2012/08/setting-up-the-raspberry-pi-the-basics/ "http://gregwoods.co.uk/2012/08/setting-up-the-raspberry-pi-the-basics/")

## Install Apache

<pre>sudo apt-get install apache2 php5 php5-gd php5-sqlite libcurl4-openssl-dev php5-curl php5-common php-xml-parser sqlite</pre>

Test the webserver works. Can browse to http://<your-ip-address>

## Set up the USB disk for OwnCloud

  * Format the disk as NTFS
  * Plug it into the RaspberryPi

<pre>sudo mkdir /media/disk</pre>

  * Check user id with

<pre>sudo nano /etc/passwd</pre>

user ‘pi’ probably has an id of 1000

  * Check disk device name with

<pre>sudo parted</pre>

<pre>   print all</pre>

shows disk is /dev/sda and partition number is 1  (in my case)

<pre>quit</pre>

<pre>sudo nano /etc/fstab</pre>

Add an entry...

<pre>/dev/sda1 /media/disk ntfs permissions 0 0</pre>

save and quit nano

<pre>sudo mount /media/disk</pre>

<pre>sudo mkdir /media/disk/web</pre>

<pre>sudo chown -R www-data:www-data /media/disk/web</pre>

#a chmod doesn’t seem to be needed, it already has 0770 permissions

## Install OwnCloud

<pre>sudo apt-get install sqlite</pre>

  * check latest release at http://download.owncloud.org/releases

<pre>sudo wget http://download.owncloud.org/releases/owncloud-4.0.7.tar.bz2
 sudo tar -xjf owncloud-4.0.6.tar.bz2
 sudo cp -r owncloud /var/www
 sudo chown -R www-data:www-data /var/www/owncloud</pre>

## Upgrading OwnCloud

NOTE: I've only done this once, so I'll ikely find a better way of doing it next time.  
This method doesn’t preserve config - try preserving it next time.  
Looks like it rescans the folders, possibly recreating the database  
COnfig is in /var/www/owncloud/config  
Maybe need to compare old and new config files after an upgrade

Probably best to disconnect all clients. Not sure if possible to do this from the server. Stopping apache would likely do it.

Delete the extracted owncloud files, and the owncloud installation

<pre>sudo rm -r ~/owncloud
sudo rm -r /var/www/owncloud</pre>

Then the same instructions as a new install

## First Use / Setup of OwnCloud

  * http://<you-ip-address>/owncloud/
  * You MUST choose the advanced settings
  * Create admin user and password
  * location of data is:  /media/disk/web

## ToDo

<pre>sudo apt-get install php-apc</pre>

to speed things up in php

&nbsp;

Now go and download an OwnCloud client, and enjoy your local network DropBox-like functionality

&nbsp;