---
id: 483
title: Snooping on Live Arduino Serial Communication
date: 2015-01-25T16:10:55+00:00
layout: single
guid: http://gregwoods.co.uk/?p=483
permalink: /2015/01/snooping-on-live-arduino-serial-communication/
categories: microcontroller programming 
---

Using the Arduino IDE, we can bring up the Serial Monitor to send and receive data from the Arduino. However, if you're using Windows, this completely ties up the COM port so that it cannot be used for anything else. If your Arduino needs to communication with other piece of software on your PC, that software gets exclusive access to that port so you can no longer use the Serial Monitor. Needless to say, it would be very nice to be able to peek at real data being sent between your PC app and the Arduino. A reliable way I've found to do this in Window is using com0com and hub4com. Here's how it works.

## Note on driver types **(it is relevant!)**

On Windows 8.1 64 bit (and true for 64 bit Vista and Win7 as far as I know) you have 3 types of driver...

  * Signed driver - This is preferred. It is how you are used to installing and using windows devices, but the developer must pay for it to be signed. Not an option for com0com.
  * Unsigned driver - every time you want to use the unsigned virtual COM ports, you must reboot your PC twice to get to the Allow Unsigned Driver option. It is a pain. This is true of the latest com0com 3.0.0.0. If using 64bit Windows, avoid like the plague
  * Test Signed Driver - you can run a simple command line instruction to tell Windows to allow Test-Signed drivers. The setting persists between reboot, so it is convenient. For com0com, this is true for the signed version of 2.2.2.0

## Installation

Use version 2.2.2.0 because it is signed. When installing, I unchecked the option to add a default pair of COM ports. I preferred a clean start Run the command: bcdedit -set TESTSIGNING ON Once com0com is installed, go and get hub4com, unzip, rename the readme file and copy the whole lot into your com0com folder.

**<span style="font-size: 1.17em; line-height: 1.5em;">Note:</span>**

<div>
  <div>
    v2.2.2.0 signed doesn't have the graphical setupg program, so need to use setupc for everthing
  </div>
  
  <div>
    com0com command prompt: list
  </div>
</div>

## My Scenario

I have an Arduino on COM3, and some PC Software which talks to it, called "PC Lap Counter" (PCLC) - it's a race management solution for slotcar racing. PCLC sends race and lap info to the Arduino over the serial connection, but I want to be able to look in on this info as it is happening.

### Step 1: Setup the Virtual COM port Pairs

<div>
  <div>
    Set up 2x com0com pairs using the com0com command line setupc.exe
  </div>
  
  <div>
  </div>
  
  <div>
     command> <span style="font-family: 'Courier New';">install 0 PortName=COM5 -</span>
  </div>
  
  <div>
     command> <span style="font-family: 'Courier New';">install 1 PortName=COM6 -</span>
  </div>
  
  <div>
  </div>
  
  <div>
    <div>
      <div>
        maybe need another COM port for a second putty session for injecting input
      </div>
      
      <div>
      </div>
      
      <div>
      </div>
      
      <div>
         COM5 is to be used by PC Lap Counter, and is paired with CNCB0
      </div>
      
      <div>
         COM6 is used by Putty for monitoring, and is paired with CNCB1
      </div>
      
      <div>
         COM3 is physical COM port which Arduino is attached to
      </div>
      
      <div>
      </div>
      
      <div>
        Note that these COM ports will persist after reboot, whereas the hub4com routes need making every time.
      </div>
    </div>
  </div>
</div>

### Step 2: Join the COM port pairs together with hub4com's Routes

<div>
  <div>
    From std command prompt...
  </div>
  
  <div>
  </div>
  
  <p>
    <span style="font-family: 'Courier New';">    hub4com -baud=9600 -octs=off -ox=on -route=0,2:All -no-default-fc-route=0,1:All \\.\CNCB0 \\.\CNCB1  \\.\COM3 </span>
  </p>
  
  <div>
  </div>
  
  <div>
    unsure what the -no-default-fc-route is all about. Try without!
  </div>
  
  <div>
    This routes PC Lap Counter to both Putty and Arduino. Plus, routes Arduino serial output to Putty
  </div>
</div>

### Step 3: Snoop away

Using Putty, create a new 'Serial' connection. In the above example, it is connected to COM6 at 9600baud

