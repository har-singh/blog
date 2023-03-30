---
layout: post
title: Azure Private Link notes
date: 2022-07-21 16:47
author: learninghar
comments: true
categories: [azure, notes, thoughts, Uncategorized]
---
<!-- wp:paragraph -->
<p>Notes and thoughts while reading https://journeyofthegeek.com/2020/03/05/azure-private-link-and-dns-part-1/</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Azure Web app run on hardware and platform managed by Microsoft so it's not automatic to assign them NICs from private Virtual Networks.</li><li>Azure Services (PaaS) are designed to be consumed/used from Internet. Otherwise why would you have the service on the platform? Answer would be: to make use of native capabilities and not have to manage the vm.</li></ul>
<!-- /wp:list -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>Last September [2019] Microsoft released the Azure Private Link service. One of the primary drivers behind the introduction of the service was to address the customer demand for secure and private connectivity to Azure services such as Azure SQL and Azure Storage as well as third-party services. Azure PaaS services used to be accessible only via public IP addresses which required a path out to the Internet. From a network security perspective, your only option to use the firewall feature built into many of the services to filter the IPs allowed to communicate with the service. While technically feasible, there had to be something better.</p><cite>Journey Of The Geek</cite></blockquote>
<!-- /wp:quote -->
