---
title: "First time contributing to the Linux Kernel"
date: 2024-04-22 
categories: [Linux Kernel, IIO, MAC0470, Patch]
tags: [linux, kernel, iio, patch]
---

## How I got here

As someone who values very much the philosophy of Free Software, I was eager to take the MAC0470 -
Free and Open Source Software Development course at IME-USP, since it meant an opportunity to give a
bit back to this wonderful universe that has helped me so much through my years learning Computer
Science. Maybe it could be a regular thing for me, to do what I can to help Free Software thrive over
closed-source alternatives.

## The challenges I had ahead

I have been using Linux as my main operating system for 3 years, and I can safely say that most of the
time I can find my way in it to do the things I want. Not like second nature, but I have gotten well
used to the environment, and thanks to courses like MAC0422 - Operating Systems, I have a good
conceptual understanding of what is going on in my computer when it is running processes, writing and
reading files, that sort of thing.

However, I had yet to dwelve in the sort of code that kept this whole environment alive. I was really
curious about where we would start meddling with Kernel code. At this point, we learnt about how the
Linux Kernel followed a monolithic architecture and was composed of various modules, and that we would
first contribute to the IIO (Industrial Input/Output) subsystem, which deals with devices that in a sense perform either
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
studied at the Operating Systems course. We used `qemu` and `libvirt` to run and manage virtual machines.

Then, we were introduced to the Kernel module system, and how to compile it with any module we want,
as well as activate them once we booted the OS using our custom Kernel. It was fun seing the whole
process involved into coding some Kernel functionality, registering it as a module, then compiling the
Kernel with it. No problems in this step, which was good, since it would become a standard loop in our
development cycle.

Afterwards, we were taught how to submit a patch to the Linux Kernel. It came as a big surprise that
no cloud service to store code like Github or Gitlab is used, but instead, it all happens through
email lists! Patches are sent to subsystem maintainers, where they follow a chain of revision until
they're integrated to production code. It feels like an obsolete thing, but if it works, it works.

Finally, we moved on to the real thing: it was time to make our own patch to a Kernel module and
submit it officially.

## The Patch

Me and my colleague [Gustavo](https://gust-vaz.github.io/) --- in this course, we work in pairs --- ended up chosing to work in the IIO
subsystem, as the tutorials were all focused in it. The other sugestion was to submit a
patch to the DRM (Direct Rendering Manager) subsystem, which is used to send comands and data do
modern GPUs, which seemed more interesting to me, but would involve learning about its maintenance
environment, as every Kernel subsystem has its own "way of doing things".

Fortunatelly for us, the professor and student assistants provided a document with some patch
suggestions, and we ended up chosing to solve a code duplication problem

### The Problem

In the file `drivers/iio/accel/kxcjk-1013.c`, there are two functions that share roughly 90% of the
code, namely: `kxcjk1013_setup_any_motion_interrupt` and `kxcjk1013_setup_new_data_interrupt`. The
only differences are an extra function call to check its return value in
`kxcjk1013_setup_new_data_interrupt`:

```c
ret = kxcjk1013_chip_update_thresholds(data);
	if (ret < 0)
		return ret;
```

and the use of different constants to manipulate the value of the `ret` variable:

```c
/* in kxcjk1013_setup_any_motion_interrupt: */

    if (status)
        ret |= KXCJK1013_REG_CTRL1_BIT_WUFE;
    else
        ret &= ~KXCJK1013_REG_CTRL1_BIT_WUFE;
        
/* in kxcjk1013_setup_new_data_interrupt: */

    if (status)
        ret |= KXCJK1013_REG_CTRL1_BIT_DRDY;
    else
        ret &= ~KXCJK1013_REG_CTRL1_BIT_DRDY;
```

### The solution

Our idea was to unify both functions into one, adding a flag (a `bool` variable named `new_data`) to its arguments, and
diverge the execution path according to the flag's value. This way, we deleted a bunch of unecessary
lines, and adjusted the function's calls throughout the code (there were only 3 of them) to accomodate
the changes made.

Then, it was time to properly format the patch, writing a commit message and emailing it to the
professor and his assistants for them to review our work. Our commit message was written as follows:

```
iio: accel: kxcjk-1013: Deduplicate setup interrupt functions

The contents of kxcjk1013_setup_any_motion_interrupt and
kxcj1013_setup_new_data_interrupt are very similar. An update was made
to merge them into one function with an additional flag indicating if
it's a new data interrupt.
```

Then, I had problems using SMTP to send the patch email with `git send-email`, as my credentials
weren't being recognised for some reason I still haven't figured out. So, Gustavo had do send it, and
we already got (mostly positive) feedback. Now, we will make the adjustments suggested and finally
send it to the IIO subsystem maintainers, hoping that our patch will be accepted and be part of the
Linux Kernel.

