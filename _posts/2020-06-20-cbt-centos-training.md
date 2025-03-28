---
layout: post
title: CBT CentOS Training
date: 2020-06-20 16:43
author: har-singh
comments: true
categories: [bash]
---

- `telinit <run-level>`  
  - `0` - halt  
  - `1` - single user (to reset the password)  
  - `6` - reboot  
- Root prompt is `#`, user prompt is `$`
- Common commands:  
  - `whoami`  
  - `apropos`  
  - `tar` (tape archive: `-cvf` for create, `-xvf` for extract)
- File manipulation:  
  - Working with text  
  - Soft links, hard links, `.`, `..`
- Monitoring system performance:  
  - `top`: Use `>` to switch from highest CPU usage to highest RAM usage; watch for `wa` (wait time)  
  - `iotop`: Check for disk swap and I/O usage when wait time is high  
- Process management:  
  - `pkill`: Finds and kills processes by pattern (e.g., `pkill fox` for Firefox)  
  - Safer alternative: Use `pgrep` first to list processes before running `pkill`  
- Process priority:  
  - "Santa Claus has a really big nice level, but he runs slowly" (nice levels affect priority)
- `su` stands for **substitute user**, not **superuser**
