---
title: "My experience contributing to KDE"
date: 2025-06-25
categories: [KDE, Spectacle, MAC0470]
tags: [linux, kde, mac0470]
---

## How I got here

Now, after contributing for the IIO subsystem of the Linux Kernel, it was time to move on to another
project. In the class, we were told that we could choose some other project that was at least related
to the Linux Kernel / part of its ambient. Me and my partner opted to contribute to some project of
KDE, since I use its desktop environment and would love to be part of its develoment. 

## What we did

We first tried contributing to Spectacle, KDE's screenshot capture utility. When searching for easy issues for first-time contributors, we came along one regarding the
aforementioned software. It was about the program not saving its window size when closed and opened up again, a behavior found in every other KDE software (try opening
a Dolphin window, for example, changing its window size, closing it, and opening it again. It will open a window with the last size it had before being closed by
default). As further detailed in the [Challenges faced](#challenges-faced) section, it did not work out.

As of June 25th, we still could not make a contribution to the KDE project, since our first attempt failed, and we are still searching for another issue we can work
on, with some candidates on the line.

## Challenges faced 

First of all, there was no tutorial we could follow to understand the development environment of KDE
and how to do things for it --- where to find developers / maintainers, where to find issues we could
work on, how to build its applications and dependencies, and the list goes on ---, so, naturally, the
first challenge we had to face was to discover all of that. Fortunately for us, the KDE project and
comunity is well structured and welcoming to new contributors, so there were pages on their wiki
teaching on how choose on what to contribute, where to find and talk with the developers --- that's done
through Matrix, an open-source distributed real-time communication network which I found to be a very
convenient way to get in touch with other people involved in the project, at least better than emails
---, how to build specific kde applications, and others.

Another problem arose when trying to build Spectacle to solve its problem of not saving the window
size when closed, as kde-builder was not being able to use the most recent version of QT, which in my
case was just not available through `apt`. We then installed the newest version manually and changed
configuration files for it to work, and that was the beginning of a series of trial and error attempts to build it and finding out we hadn't some library in the newest
version on our systems. After many (many) days and attempts, we finally had a locally-built version of Spectacle! We had installed by hand many libraries in versions `apt` did not
have available, and it was finally time to test the program in its newest version (the one in the `master` branch of its repository) and begin development!

Unfortunately, that was not what happened, as we stumbled upon a worse problem: our build of Spectacle did not have permission to take screenshots... And that alone
would not be a problem if we could resize its window, but it turned out we could not. First, we tried searching in forums for solutions to our problem: in all of them,
people were having *slight* variations of the error we were having, and it was related to other aspects of their setup --- like using Wayland instead of X11. After
many failed attempts to make it work, we then seeked help in the KDE Matrix room for developers: I explained my issue, hoping that it was a common problem for
developers and
that it had an easy solution. Actually, it seemed like a common problem: Spectacle needs to be installed on the same prefix where the running instance of KWin lives.

![Nate-Graham-describes-solution-for-spectacle-permission-issue](/assets/img/kde-development/kde_spectacle_kwin.png)

With that in mind, we tried once more installing Spectacle where our running instance of KWin was, but that was not with its challenges. First of all, we ran into
superuser permission issues, which was fair, since we were trying to install locally-build software in locations reserved to package managers and the such. After
changing kde-builder's configuration file to run commands with sudo by default, we ran into another problem: all of a sudden, we could not build Spectacle again, as
some libraries it required were not installed or in their latest version, which was very strange. After again going through the process of trial and error for
installing the libraries required, we thought: "hey, maybe we should be running a more cutting-edge setup. For instance, one that at least runs the Plasma 6 desktop
environment. That way, we should have all the libraries KDE software need to be built, and in their latest versions".

With that in mind, we set off to setup our development setups: my partner even installed KDE Neon with Plasma 6 on his laptop, while I stuck with an Arch Linux virtual
machine in VirtualBox (biggest mistake). While I could not build Spectacle because of many problems in my development environment (mainly things that I needed to
install manually because I stuck with Arch), my partner could build Spectacle rather easily, but he had the same problem of screenshot permissions. With that, we
thought that maybe it was a better idea to search for issues in other KDE softwares, ones we could build and run easily, like Dolphin, and left Spectacle's window
resizing issue as it was.
