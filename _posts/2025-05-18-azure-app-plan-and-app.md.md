---
layout: post
title: Azure App Service Plan vs Function App Containers – Clearing the Confusion
date: 2025-05-23 09:48
author: har-singh
comments: true
categories: [blog]
---

While working with Azure Function Apps (Python in particular), a recurring point of confusion was understanding how **App Service Plans** relate to **containers**. Here's a quick rundown based on actual experience.

## App Service Plan – Not a Container

An **App Service Plan** defines the compute environment:
- CPU and memory allocation
- Operating system (Linux or Windows)
- Pricing tier and region

It’s essentially a virtual machine pool that hosts your apps. Importantly, **the plan itself is not a container**.

## Function Apps – Containerised by Default

When a **Python Function App** is deployed (especially on a Linux plan), Azure automatically runs it inside a **container**. No container configuration is needed — it’s just how Azure handles Python (and other languages) in the backend.

This behaviour initially caused confusion. Despite not defining any Docker image or container setup, container instances were spinning up behind the scenes.

### Reasons for this:

- Isolation: Each Function App runs in its own sandbox
- Portability: Easier for Azure to manage runtime environments (Python, Node, etc.)
- Better portability and scaling management for Azure

## What’s Actually Happening?

Consider this setup:
- One **App Service Plan**
- Three **Python Function Apps**

The outcome:
- Azure provisions VM resources for the plan
- Each Function App runs in its **own isolated container**
- All containers share the same VM infrastructure provided by the plan

So, the Function Apps are containerised, but the App Plan is just the shared compute layer.

## Custom Containers?

Yes — if more control is needed, a **custom Docker container** can be deployed (typically with a Premium Plan or using custom handlers). But even in standard deployments, Azure is already using containers behind the scenes.

## Summary

An **App Service Plan** provides compute — not a container. Each **Function App** runs in a separate, Azure-managed container. No manual configuration is required unless customisation is desired.

This setup allows Azure to offer isolation, scaling, and flexibility out of the box. Hopefully this clears up the confusion — it certainly did for me.
