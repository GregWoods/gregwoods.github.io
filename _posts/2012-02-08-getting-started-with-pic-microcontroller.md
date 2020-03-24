---
id: 286
title: Getting Started with PIC Microcontroller
date: 2012-02-08T10:10:45+00:00

layout: single

guid: http://gregwoods.co.uk/?p=286
permalink: /2012/02/getting-started-with-pic-microcontroller/
categories:
  - Microcontroller
  - Programming
---
A couple of years ago I bought a PICKit2 for the princely sum of £5 including postage. It was a special offer from Microchip that I couldn't refuse. I'd tinkered with the Atmel AVR chip in the past, but liked the on-board USB features of the Microchip  PIC18F range. I knew it would be useful for some custom [HID](javascript:void() "Human Interface Device, e.g. keyboard, mouse, joystick") devices for Flight Simulator one day.

Anyway, I've got a simple alarm clock idea which wakes you up by gradually increasing the brightness of an LED strip light behind the headboard of the bed. As a minimum, it needs a simple microcontroller, a real time clock (RTC) of some sort, one or more power transistors for the LEDs, and an LCD screen and buttons for the UI. If I wanted to get this thing done quickly, I'd probably go for an Arduino solution - there are less hardware options and more really good demos and tutorials. However, I already have this PICKit2, and learning the raw nuts and bolts of the PIC range will allow me to avoid the cost of a £20 Arduino in every project.

## The Hardware

  * PICKit2 programmer, which I believe has [ICD](javascript:void() "In Circuit Debugging") capabiities
  * 44-pin demo board. This has a PIC16F887 onboard, some LEDs and a potentiometer

## The Software

Installed in this order

  * Java SE Runtime version 6 (32 bit version, despite being on 64bit OS) (version 7 doesn't seem to work with MPLAB X)
  * MPLAB X from Microchip - don't download the compilers from this page, they are never the most up to date
  * HI-TEC C compiler for PIC10,12,16 (version 9.83 as of Feb 2012, signin required)
  * HI-TEC C compiler for PIC18 (version 9.80 as of Feb 2012, signin required)
  * Microchip PICKit2 programmer (latest is v2.61 in Feb 2012)

## First Test

<img src="http://gregwoods.co.uk/wp-content/uploads/2012/02/PICKit2Programmer100pc.png" alt="" title="PICKit2 Programmer" width="554" height="675" class="alignright size-full wp-image-294" /> 

Although, I want to be writing my own code in C, to test the environment is working, I will first send a pre-compiled HEX file to the demo board, and test.

  * Hit the "Auto Import Hex + Write Device" button
  * Choose a demo file from **C:\Program Files (x86)\Microchip\PICkit 2 v2\DBE Demo\16F887Demo.HEX**
  * The programmer should erase and then program the chip, but you won't see anything happen
  * You must manually supply power to the board using the 'VDD PICkit2&#8242; 'On' checkbox

I must have spent 2 hours programming and reprogramming the device wondering why the demo wasn't running. Eventually I tried the 'VDD PICKit2&#8242; 'On' option, hoping it wouldn't fry my board, and it worked instantly. I'll put it down to bad UI design of the PICkit2 Programmer - it's clearly designed with Microchip engineers in mind, and not Joe Public. The help file, whilst technically accurate, needs to spell it out clearly: "Once you have programmed your demo board, you need to supply it with power. The PiICkit2 can do this for you, but you need to tell it using this option [big arrow pointing to diagram]".

Other pre-compiled demos can be found on the PICkit2 CD-ROM, in the **44Pin Demo Board** folder.

The second test (in the next post) is to compile a sample [ASM](javascript:void() "assembly language source file") in MPLAB X, upload to the demo board, and run it.