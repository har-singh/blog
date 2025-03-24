---
layout: post
title: "Red Hat training for Linux basics"
date: 2020-04-03 12:57
author: har-singh
comments: true
categories: [basics, learning, linux, red hat]
---

I've just learned that the `usr` directory on Linux/UNIX systems stands for UNIX System Resources. I always assumed that `usr` was an abbreviation for user. So another lesson is (or a refresher) is that you should never assume.

Second thing learned is that there are two independent `/tmp` directories in Linux. One is `/tmp` and the other is in `/var/tmp`. The important thing I didn’t know before is that the content of `/tmp` is deleted automatically. A file in `/tmp` will be removed automatically after ten days, while the file in `/var/tmp` will be removed after thirty days.

These are basics, but basics are important.

All learned thanks to the Red Hat Enterprise Linux Technical Overview course - lesson The File System Hierarchy. Thanks to Red Hat for making the material available for free (temporarily) at [https://www.redhat.com/en/services/training/rh024-red-hat-linux-technical-overview](https://www.redhat.com/en/services/training/rh024-red-hat-linux-technical-overview).
