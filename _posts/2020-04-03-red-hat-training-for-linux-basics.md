---
layout: post
title: Red Hat training for Linux basics
date: 2020-04-03 12:57
author: har-singh
comments: true
categories: [basics, learning, linux, red hat]
---

I've just learned that the `usr` directory on Linux/UNIX systems stands for UNIX System Resources. I always assumed that `usr` was an abbreviation for 'user'. Another lesson here: never assume.

The second thing I learned is that there are two independent `/tmp` directories in Linux. One is simply `/tmp`, and the other is located in `/var/tmp`. The important thing I didn’t know before is that the contents of `/tmp` are deleted automatically after ten days, while files in `/var/tmp` are removed after thirty days.

These are basic concepts, but basics are important!

All of this was thanks to the Red Hat Enterprise Linux Technical Overview course – specifically the lesson on The File System Hierarchy. Huge thanks to Red Hat for making this material available for free (temporarily) at [rh024 redhat.com](https://www.redhat.com/en/services/training/rh024-red-hat-linux-technical-overview)
