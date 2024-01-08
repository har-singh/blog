---
layout: post
title: High throughput ethernet ASICs by Justin Pietsch
date: 2020-09-24 18:13
author: learninghar
comments: true
categories: [asic, notes, openflow, technical]
---
<!-- wp:image {"id":256,"sizeSlug":"large"} -->
<figure class="wp-block-image size-large"><img src="assets\imgs\soc-size.jpg" alt="" class="wp-image-256" /><figcaption>My Raspberry's chip size: 10x10 mm</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Harpreet's notes on <a rel="noreferrer noopener" href="https://elegantnetwork.github.io/posts/A-Summary-of-Network-ASICs/" target="_blank">A summary of High Speed Ethernet ASICs</a> written by Justin Pietsch:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Chip Reticle limit is 33x26 mm, absolute max size 858mm^2. Nvidia’s next gen chip GA100 is 54.2 billion transistors and a die size of 826mm^2 using 7nm processor node.</li><li>for prospective my RaspberryPi's chip is 10x10 mm (picture).</li><li>network ASICs are as big as the GPU</li><li>When talking about Integrated Circuits (ICs), IP means Intellectual Property</li><li>the author does not see the need for programmable pipeline, especially for openflow</li><li>author would be wary of using Cisco as a provider, they’ve not done this before and it doesn’t fit their regular business model but have faith in Dune/Leaba team</li></ul>
<!-- /wp:list -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>"As networks get large, the cost of the network is driven by the cost of the optics. The real money saving is not when you get a faster chip, but when the chip supports higher throughput SERDES."</p><cite>Justin Pietsch</cite></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->
