---
layout: post
title: Azure Private Link notes
date: 2022-07-21 16:47
author: har-singh
comments: true
categories: [azure, notes, thoughts]
---

Notes and thoughts whilst reading [Azure Private Link and DNS](https://journeyofthegeek.com/2020/03/05/azure-private-link-and-dns-part-1/).

- Azure Web Apps run on hardware and platforms managed by Microsoft, so they don’t automatically get NICs from private Virtual Networks.
- Azure Services (PaaS) are designed to be consumed/used from Internet. Otherwise why would you have the service on the platform? Answer would be: to make use of native capabilities and not have to manage the vm.

> Last September [2019] Microsoft released the Azure Private Link service. One of the primary drivers behind the introduction of the service was to address the customer demand for secure and private connectivity to Azure services such as Azure SQL and Azure Storage as well as third-party services. Azure PaaS services used to be accessible only via public IP addresses which required a path out to the Internet. From a network security perspective, your only option to use the firewall feature built into many of the services to filter the IPs allowed to communicate with the service. While technically feasible, there had to be something better.  
> — Journey Of The Geek
