---
layout: single
title:  "Why Learn Embedded Rust on the STM32F103 Blue Pill"
date:   2020-03-12 19:32:31 +0000
categories: microcontroller embedded rust stm32 bluepill
published: true
---

![STM32F103 Blue Pill on a breadboard]({{ site.url }}{{ site.baseurl }}/assets/images/bluepill-in-breadboard.jpg)

I have spent quite a bit of time recently trying to learn the Rust programming language for use on the $2 ARM Cortex M3 STM32 board, commonly known as the "Blue Pill". The learning process has often been frustrating, and it has not been quick. But I feel I can share some code, and tips which can make it less painful.

# Where have I come from?

I am a full time developer working on the Microsoft stack for a number of years in the high level C# realm. As a hobbyist, I have a strong interest in microcontrollers, and have tinkered with PIC and AVR using assembly language, C, and Arduino. I love the Arduino platform due to it's accessibility for noobs, but I've been itching to move away from it. Why?

# Why the Blue Pill?

## Cost

For the same price as an 8MHz 8bit Arduino Pro Mini clone, I can buy a 72MHz, 32 bit Arm Cortex M3 board (and for not much more, a Cortex M4F)

## Features

For my projects, both Arduino and Arm Cortex M3 boards will have all the features I need, but the stm32 boards have greater horsepower, which allows the running of a simple RTOS, along with more complex code in interrupt handlers.

## Debugging

It is possible to do real debuggiong on the stm32 board, when connected to an ST-Link debugger. It should be possible to stop using printing-to-the-console to debug, and instead set breakpoints and step through the code like a real programmer!

# Why Rust?

I love the simplicity of Arduino code. This simplicity is all due to the friendly design of the libraries. But, it is still C++, and once your code starts getting even slightly complex, you hit all the problems of C++, including various abuses of pointers which cause hard to find runtime bugs. 
Rust promises the speed of C/C++ with a more robust system of memory safety, whereby the compiler always knows which code block a variable belongs to, and thus can check for many sources of bugs at compile time (this is a gross oversimplification. Go and read the docs yourself)
I don't have the clout to convince anyone that Rust is worth the effort, but you have to at least check it out. Start with the official docs [rust-lang.org/what/embedded](https://www.rust-lang.org/what/embedded)

It also helps that Rust has a very helpful compiler. Compiler error messages are not the afterthought that they are in C++. They system has been carefully thought out, and is exceedingly helpful to noobs.

# The Trap

It is always dangerous to learn a new tool or lanaguage and then use it for absolutely everything, no matter how inappropriate it may be. For some projects, an 8 bit microcontroller on Arduino may be the best choice. But, to maximise the little time I have for learning the new platform, I will be focusing my efforts on Rust on the STM32 for current hobby projects.

[Next - How to Learn]({% post_url 2020-03-29-how-to-learn-embedded-rust-on-the-stm32f103-blue-pill %})
