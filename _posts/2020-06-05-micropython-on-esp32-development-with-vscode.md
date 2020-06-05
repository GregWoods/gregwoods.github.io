---
layout: single
title:  "MicroPython on ESP32 Development with VS Code"
date:   2020-06-05 06:49:00 +0000
categories: microcontroller embedded micropython esp32
excerpt: Once you have working MicroPython firmware on an ESP32 board, you need to write code. You can't stay in REPL forever, so lets set up our developer environment using Visual Studio Code
permalink: 2020-06-05-micropython-on-esp32-development-with-vscode
published: true
---

> **UPDATE:** This post is a work in progress, it reflects my current thinking on the best way to start and run a micropython project on an ESP32, but I've been looking into this for only a few days, so it may change a lot. 

PREVIOUS: Flashing the MicroPython firmware on an ESP32

* Notes: WORK IN PROGRESS: tidy up later
* ToDO: Add header image with board and micropython logo

## Be Organised!

Don't just dump your code anywhere, make a decision about where to put it! For me, this is **C:\Users\Gregw\microcontroller-home**


From Windows Terminal

* Set up folder structure. Adjust to taste! Don't forget the tab key to autocomplete partial folder and file names.

```dos
cd \Users\gregw\
mkdir microcontroller-home
cd microcontroller-home
```

Getting to a REPL prompt is a good start, but you need to be able to write code in a capable editor, with intellisense, or context-aware auto-completion, because you're 50x more productive when you can type a dot after the name of an object, and your editor suggests all applicable properties and methods on that object. Without this, you'll be spending over 99% of your time trawling documentation.

>I've tried out VS Code extensions for ```ampy```, ```rshell``` and the ```MicroPython IDE```, with varied degrees of success (tip: don't bother even trying the MicroPyhton IDE in Windows, it does nothing).

The Best Options I can find are...

* micropy-cli
* Pymakr

## Global Setup

* It is assumed you've installed all the prereqs listed in the previous post
* [Install NodeJs](https://nodejs.org/en/download/)
  * use the LTS version, 64bit msi for Windows
  I also accepted the recommendation to install additional tools, which includes the  windows package manager "chocolatey"

I've chosen to install the following globally, as you will likely use
these tools in many projects.

|I am also not using virtual environments for each project, 
since micropython dependencies are managed separately by micropy-cli.

```dos
cd c:\users\gregw\microcontroller-home
pip install esptool micropy-cli
micropy stubs search "esp32"
micropy stubs add "esp32-micropython-1.12.0"
```

## New Project Setup

Blinking an LED is the Hello World of the microcontroller world.

These step apply to all new projects. I am using a separate python virtual environment for each project, which is a couple more steps for each projec, but keeps each project nicely self-contained.

After a *lot* of thought, I've decided on the following project naming convention...

*projectname-device-platform/language*

Once you get hundreds of projects stacking up, you come to realise that good naming matters a lot. More on naming in another post.

```dos
micropy init oled-esp32-upy
    select all 5 options using space bar and up/down arrows, with Enter to Ok your selection
    then select the stub: esp32-micropython-1.12.0
cd oled-esp32-upy
code .
```

When VS Code opens, it will ask if you want to install the recommended Extensions. Go ahead and do it.

I will not be using VS Code's Workspaces feature, but if you regularly switch between different types of projects e.g. Rust and MicroPython, Workspaces are extremely useful.

* Install the VS Code **PyMakr** extension

## Each Session

Once the above steps have been done once in a project folder, next time you want to work on that same project, you just need to navigate to that folder and start VS Code.

```dos
cd c:\users\gregw\microcontroller-home\oled-esp32-upy
code .
```

## Add Code

TODO: show something on the onboard OLED

```python


```

## References

[Setup **microPy** and **PyMakr** in VS Code](https://lemariva.com/blog/2019/08/micropython-vsc-ide-intellisense)
