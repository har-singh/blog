---
layout: post
title: High throughput ethernet ASICs by Justin Pietsch
date: 2020-09-24 18:13
author: har-singh
comments: true
categories: [asic, notes, openflow, technical]
---

![My Raspberry's chip size: 10x10 mm](/assets/imgs/soc-size.jpg)
*My Raspberry's chip size: 10x10 mm*

Harpreet's notes on [A summary of High Speed Ethernet ASICs](https://elegantnetwork.github.io/posts/A-Summary-of-Network-ASICs/) written by Justin Pietsch:

- Chip Reticle limit is 33x26 mm, absolute max size 858mm². Nvidia’s next gen chip GA100 is 54.2 billion transistors and a die size of 826mm² using 7nm processor node.
- For perspective, my RaspberryPi's chip is 10x10 mm (see image).
- Network ASICs are as big as the GPU.
- When talking about Integrated Circuits (ICs), IP means Intellectual Property.
- The author does not see the need for a programmable pipeline, especially for OpenFlow.
- The author would be wary of using Cisco as a provider, as they’ve not done this before and it doesn’t fit their regular business model but has faith in the Dune/Leaba team.

> "As networks get large, the cost of the network is driven by the cost of the optics. The real money saving is not when you get a faster chip, but when the chip supports higher throughput SERDES."  
> — Justin Pietsch
