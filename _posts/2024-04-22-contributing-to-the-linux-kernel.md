---
title: "First time contributing to the Linux Kernel"
date: 2024-04-22 
categories: [Linux Kernel, IIO, MAC0470, Patch]
tags: [linux, kernel, iio, patch]
---

### How I got here (maybe think of a better title)

As someone who values very much the philosophy of Free Software, I was eager to take the MAC0470 -
Free and Open Source Software Development course at IME-USP, since it meant an opportunity to give a
bit back to this wonderful universe that has helped me so much through my years learning Computer
Science. Maybe it could be a regular thing for me, to do what I can to help Free Software thrive over
closed-source alternatives.

### The challenges I had ahead

I have been using Linux as my main operating system for 3 years, and I can safely say that most of the
time I can find my way in it to do the things I want. Not like second nature, but I have gotten well
used to the environment, and thanks to courses like MAC0422 - Operating Systems, I have a good
conceptual understanding of what is going on in my computer when it is running processes, writing and
reading files, that sort of thing.

However, I had yet to dwelve in the sort of code that kept this whole environment alive. I was really
curious about where we would start meddling with Kernel code. At this point, we learnt about how the
Linux Kernel followed a monolithic architecture and was composed of various modules, and that we would
first contribute to the IIO subsystem, which deals with devices that in a sense perform either
analog-to-digital (ADC) conversion, or digital-to-analog (DAC) conversion, or both.

At this moment, we started doing "tutorials" made by students from the FLUSP (FLOSS at USP) extension
group to learn how to setup our Linux Kernel development environment and learn about IIO and Kernel
modules in general. I did not expect this much information, and was a bit overwhelmed by the amount
steps it was involved in those tutorials, but I still managed to do them and understand (although not
100%) what was happening. Even though many students in this class had problems in some part of the
process, mostly due to specifics of different operating systems and environment settings, I was lucky
to be able to do the tutorials somewhat smoothly.

First, we needed to setup a virtual environment to test our custom Kernels without using a production
one, which could be disastrous if the Kernel did not compile, or something broke when a change was
made to it. That was the first time I ever dealt with virtual machines! It was really nice to download
a Debian ISO and actualy run the OS inside a running OS at the same time I saw in practice things I
studied at the Operating Systems course.
