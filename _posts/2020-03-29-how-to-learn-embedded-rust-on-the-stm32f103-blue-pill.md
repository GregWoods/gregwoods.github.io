---
layout: single
title:  "How to Learn Embedded Rust on the STM32F103 Blue Pill"
date:   2020-03-12 19:32:31 +0000
categories: microcontroller embedded rust stm32
published: true
---

![STM32F103 Blue Pill with STLink V2 Debugger]({{ site.url }}{{ site.baseurl }}/assets/images/bluepill-with-stlink.jpg)

# The water's not _that_ deep - you'll be fine!

You will find tutorials and blog posts telling you how easy it is to get started in Rust on an STM32 platform. 

They lie!

Or at least, they are written by experienced embedded developers who are simply transitioning to Rust.
Coming from Arduino, you are used to the ease of: downloading the IDE, changing the board type, copy-pasting some demo code, change the odd pin assignment, compile and upload. Done!


# This is not Arduino

Instead you are now faced with:

* Manual setup of your toolchain
* Manual configuration of your debugging tool/uploader
* No out of the box integration with your IDE
* Blog posts which are outdated, whose code won't compile anymore
* Libraries at a much lower level than Arduino ones
* Having to be very familiar with your chip's data sheets


# The Wrong Way to Learn

My initial approach to learning, which has usually served me well, was
* Avoid any dusty official documentation, it takes too long to digest all that detail
* Find a respectable looking blog-with-code
* Relicate the steps in the blog; make some trial and error modifictions; add some interesting looking libraries to tinker with peripherals
* Glue together the various bits of experimentation into your actual project

I wasted a lot of time.
Rust and the libraries in the ecosystem have changed in the last 3 years, and most of the blog posts were written by seasoned embedded developers who were early adopters in Rust. Although I learned something from every one of them, it was not the right apporoach.


# Take Your Time, Structure Your Learning

The right way is to take your time and use the official docs - they are excellent, and shouldn't be rushed.
I am using a multi-faceted approach.
* Learn Rust on its own - with no embedded distractions 
  * [The book](https://doc.rust-lang.org/book/)
  * [Rust by Example](https://doc.rust-lang.org/stable/rust-by-example/)
  * [Rust Cookbook](https://rust-lang-nursery.github.io/rust-cookbook/) - because it's good to see how other people write Rust
  * [Lots more official Rust documentation](https://www.rust-lang.org/learn)
* [Get started with embedded Rust](https://rust-embedded.github.io/book/) Start at the beginning. Don't fast forward until you've completed the next step, QEMU 
  * [Use the emulator QEMU](https://rust-embedded.github.io/book/start/qemu.html) even if you never plan on using the emulator ever again, it helps you grasp the toolchain and ecosystem.
  * [Get your first blinky working in a VS Code environment](https://github.com/GregWoods/stm32-01-blink)  This is my own quickstart code. It is using a HAL, so it is skipping ahead a few steps, but I find it useful to have a ready to go starter project
* Learn the chip
  * [Learn about SVDs and Peripheral Access Crates using this excellent tutorial from Vivonomicon](https://vivonomicon.com/2019/05/23/hello-rust-blinking-leds-in-a-new-language/)
  * [Get to know the 1134 page Reference Manual](https://www.st.com/resource/en/reference_manual/cd00171190-stm32f101xx-stm32f102xx-stm32f103xx-stm32f105xx-and-stm32f107xx-advanced-arm-based-32-bit-mcus-stmicroelectronics.pdf). This is not optional! But you don't need to read it cover to cover. 
    * Get to understand the blinky code from the point of view of the Reference Manual. Start at chapter 9 "General-purpose and alternate-function I/Os (GPIOs and AFIOs)". Comparing the Reference Manual to the code you've written using your PAC, will help you grasp how the STM32 registers work for IO.
  * [Go and get a HAL, and learn to use it](https://github.com/stm32-rs/stm32f1xx-hal) But make sure you get the right one. There are deprecated projects out there to catch the unwary.
    * After using the Peripheral Access Crate directly, the HAL, to me anyway, is more complex and less intuitive due to it's use of the inversion-of-control principle. But, getting used to the way it works should help you write code which can be ported to other chips.
  * [Get to know RTFM - Real-Time-For-the-Masses](http://www.rtfm-lang.org/). I'm yet to get into this, but it does feel like the right way to go for most projects.

The above list is not a strict sequence, I am learning a little about each of the 3 top level areas each week. 
Progress, for me at least, is not particularly fast, which can be frustrating when you have projects in mind.
Which is why the next point helps.

# Keep a Learning Log

This has helped me to avoid the feeling that I'm not getting anywhere. It helps me see what to study and try out next. I abbreviate book titles.

I use a simple table in OneNote

Excerpt...

| Date       | Notes |
| ---------- | ----- |
| older      | Pckt RustIn7days, ch1, ch2   Got a bit stuck on Traits with Generics |
| 2020-01-29 | RBE ch1, ch2 |
| 2020-01-30 | RBE ch3   skipped linked list example |
|            | RBE ch4   variable shadowing. Not sure of the point! |
|            | RBE ch5, ch6, ch7, ch8.3 |
| 2020-01-31 | RBE ->8.5.1   Refs!! Destructuring. See also RB (RustBook) 4.1,4.2 |
| 2020-02-03 | RBE  8.5.3, 8.6, 8.7 9, 9.1   Binding... didn't really get it, but likely don't need to! |
|            | If...let  - stupid syntax, blame Swift |
|            | while...let skipped |


I've seen lots of more complex Learning logs online, but for me, just a running virtual bookmark is enough.
Notes may be a page or chapter reference. Sometimes I'll note an immportant topic I convered. I'll note any code I worked on.
My log isn't well written or consistent in its type of content. 
I don't go into great detail about what I've learnt, it isn't a summary. It is more to track progress. 

I've found it a great help.

So that is my Rust learning story so far. I hope it helps!


