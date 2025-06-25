---
title: "Taking a shot at contributing to KDE"
date: 2025-05-14
categories: [KDE, Spectacle, MAC0470]
tags: [linux, kde, mac0470]
---

## How I got here

Now, after contributing for the IIO subsystem of the Linux Kernel, it was time to move on to another
project. In the class, we were told that we could choose some other project that was at least related
to the Linux Kernel / part of its ambient. Me and my partner opted to contribute to some project of
KDE, since I use its desktop environment and would love to be part of its develoment. 

## What we did

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
configuration files for it to work, and.

<!-- falar sobre o spectacle não tendo permissão pra tirar screenshot -->
