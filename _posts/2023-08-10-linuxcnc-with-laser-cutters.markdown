---
layout: post
title:  "CNC laser cutting on Linux"
date:   2023-08-10 17:56:46 -0700
categories: tutorials
tags: CNC laser linux grbl
---

## What is GRBL?

[GRBL][grbl] is a free and open source software flashed to microcontrollers based on the ATmega 328 (such as the Arduino Uno), allowing them to easily control multi-axis motor drivers and thus a complete computer numeric control (CNC) machine.  To have a full CNC machine, one needs a controller, a motor driver, the motors, the mechanical structure with linear and/or angular guides, and a source of operation.  The source of operation can be a 3D printer nozzle.  The motor driver boards come in diverse designs and formats.  GRBL allows CNC machines to be precise and powerful while keeping their affordability.

I must say that there are several well-written guides on the topic on the internet, I don't pretend to bring new information to the table, but maybe this will be a nice summary for those who are considering building their own DIY machine, getting a commercial one, understanding a bit more of what they have in hand, or how to operate one at work using their own Linux system.

## G-code explanation

A g-code is a set of instructions to the controlling software that will be sent to the microcontroller.  If we open a generic g-code file, we will see something like
```
...
G1 X90 Y50 Z0.5 F3000 E1
...
```

We then import this code to the software installed in our computer, which will in turn send instructions to the microcontroller to operate the motors in a way specified by the g-code and complete the task given.

### What is being done "in the background"?

By running ``lsusb`` on a machine with a GRBL-powered device connected via USB, I get the output

```
...
Bus 002 Device 002: ID 1a86:7523 QinHeng Electronics CH340 serial converter
...
```

And by checking ``ls -l /dev/ttyUSB*``,
```
crw-rw----+ 1 root dialout 188, 0 Aug 15 13:53 /dev/ttyUSB0
```
indicating that a regular tty USB device is connected to the machine.

Just like any microcontroller connected via USB, we can send and receive commands by writing them to the USB tty device.  GRBL comes in 115200 and 9600.  In my case, I'm using a machine with a baudrate of 115200, so we can set the device baudrate to that with
```
stty -F /dev/ttyUSB0 115200
```
and then to listen to our system,
```
tail -f /dev/ttyUSB0
```

## Generating a g-code for a 2D project (machining or laser cutting)

Inkscape is a powerful tool to 

## Useful links and references

1. [Inkscape][inkscape]

[grbl]: https://www.grbl.org/
[grbl-git]: https://github.com/grbl/grbl
[inkscape]: https://inkscape.org/
[jtech-photonics]: https://jtechphotonics.com/?page_id=2012
[cncjs]: https://cnc.js.org/
[cncjs-git]: https://github.com/cncjs/cncjs
[bcnc]: https://github.com/vlachoudis/bCNC