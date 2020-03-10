---
id: 161
title: Head Tracking Project Begins
date: 2008-11-12T23:00:03+00:00
author: Greg Woods
layout: post
guid: http://gregwoods.co.uk/?p=161
permalink: /2008/11/head-tracking-project-begins/
categories:
  - Flight Simulation
---
Head tracking, in a flight simulator context, is where small movements of your head will change your viewpoint in the simulation. e.g. You tilt your head down slightly, and the virtual cockpit view moves down to look at your gauges. Move your head back up and slightly left, and you look out of the side window. If you want to see how well it works in practice, search youtube for fsx head tracking, or fsx trackir.

Anyway, after a little digging online, I discover that there are a lot of people who have assembled their own head tracking rig with a webcam and some LEDs. Now this is my kind of project! No hardcore electronics, no programming, just assemble all the pieces with a hot glue gun. Great!

It turns out that the Wii Controller (wiimote) is pretty much the best thing to use as your webcam. That little IR filter on the front of the wiimote actually hides a camera. It’s low-resolution, monochrome only, but runs at over 100fps for fluid movements. By interpolating the pixels it acts like a much higher resolution device. Best of all, instead of sending this video feed to the PC for it to analyse, like a regular webcam; it contains an onboard processor to isolate up to 4 sources of IR illumination (though the wii only uses 2), and send these coordinates via bluetooth to the Wii, or PC. The upshot of this is that is that it is very suitable for head tracking. And before you start laughing, no you don’t attach the wiimote to your head – you mount it in front of you, and attach either 1 or 3 LEDs to your head. 

So, I borrowed a Wiimote, got my Bluetooth dongle installed and paired them, found FreeTrack software, and soon had the animated skulls moving in response to the signal from an old remote I’d found. Using one LED you get the same movements you would from the hat switch (known as 2DOF) – though much more fluid. This will probably suffice 90% of the time. However, with 3 LEDs, you can get 6DOF, so if you shift left, right, up, down in your seat, the virtual pilot’s head moves in reponse. This would be great for getting your head close to the side window when trying to land that heli (though that may not be the recommended way to do it!) You can even cheat and have your head come out of the side of the aircraft, depending on how you’ve set it up. The other 2 axes are tilt head left and right. These are often used in First Person Shooters for looking round corners – I’m unsure about the usefulness in FSX.

It took several failed attempts before I got any movement out of FSX, but persistence paid off. It worked when I kept the Wiimote ‘talking’ to the PC all the time FSX was loading.  
Anyway, my own Wiimote is on order from Amazon, I got IR LEDs and resettable fuses (for USB power) from CPC. All I need now is a wire coat hanger! More details to follow.