---
layout: single
title:  "Learning Embedded Rust on the STM32F103 Blue Pill... Why?"
date:   2020-03-10 19:32:31 +0000
categories: microcontroller embedded rust stm32
published: false
---

I have spent quite a bit of time recently trying to learn the Rust programming language for use on the $2 ARM Cortex M3 STM32 board, commonly known as the "Blue Pill". The learning process has often been frustrating, and it has not been quick. But I feel I can share some code, and tips which can make it less painful.

## Where have I come from?

I am a full time developer working on the Microsoft stack for a number of years in the high level C# realm. As a hobbyist, I have a strong interest in microcontrollers, and have tinkered with PIC and AVR using assembly language, C, and Arduino. I love the Arduino platform due to it's accessibility for noobs, but I've been itching to move away from it. Why?

## Cost
For the same price as an 8MHz 8bit Arduino Pro Mini clone, I can buy a 72MHz, 32 bit Arm Cortex M3 board (and for not much more, a Cortex M4F)

## Features
For my projects, both Arduino and Arm Cortex M3 boards will have all the features I need, but the stm32 boards have greater horsepower, which allows the running of a simple RTOS, along with more complex code in interrupt handlers.

## Debugging
It is possible to do real debuggiong on the stm32 board, when connected to an ST-Link debugger. It should be possible to stop using printing-to-the-console to debug, and instead set breakpoints and step through the code like a real programmer!

## Language
Although I love the simplicity of Arduino code, this simplicity is all due to the friendly design of the libraries. It is still C++, and once your code starts getting even slightly complex, youy hit all the problems of C++, including various abuses of pointers which cause hard to track down bugs. 
Rust promises the speed of C/C++ with a more robust system of memory safety, whereby the compiler always knows which code block a variable belongs to, and check for potential bugs at compile time (this is a gross oversimplification. Go and read the docs yourself)

