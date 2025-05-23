---
layout: post
title: Azure App Service Plan vs Function App Containers – Clearing the Confusion
date: 2025-05-23 09:48
author: har-singh
comments: true
categories: [blog]
---

I've been working with Azure Function Apps (especially in Python), and one thing that tripped me up initially was how **App Service Plans** relate to **containers**. If you've been confused by this too, you're not alone. Here's a quick explanation based on what I've learned.

## App Service Plan – Not a Container

The **App Service Plan** in Azure is basically the **compute environment**. It defines:
- How much CPU and memory you get
- What region your app runs in
- Whether you're using Linux or Windows
- Your pricing tier

It's like the "server" behind the scenes. But here's the key point: **the App Service Plan itself is not a container**.

## Function Apps – Containers Under the Hood

When you deploy a **Python Function App** to Azure (especially on Linux), Azure runs it inside a **container** automatically. You don’t need to set this up – it’s just how Azure handles Python (and other languages) in the backend.

This was surprising to me at first – I hadn’t set up any Dockerfile or container image, but Azure still fired up a container when I deployed. Turns out, it’s by design.

### Why?

- Isolation: Each Function App runs in its own sandbox
- Portability: Easier for Azure to manage across environments
- Language support: Python works best in a controlled environment

## So What’s Actually Happening?

Let’s say you have:
- One **App Service Plan**
- Three **Python Function Apps**

What happens:
- Azure creates one or more VMs for the App Service Plan
- Each Function App runs inside its **own container** within those VMs
- They **share the same underlying compute** (memory, CPU), but are isolated at the container level

You’re not dealing with containers directly, but they’re there.

## Can You Use Your Own Container?

Yes – if you want full control, you can deploy a **custom Docker container**. This is usually done with the **Premium Plan** or **Consumption Plan with custom handlers**.

But even if you don’t, Azure is already containerising your app for you under the hood.

## Final Thoughts

If you're like me and thought "is the App Plan the container?", the answer is **no**. The App Plan is just the compute. The actual container magic happens at the **Function App** level – quietly and automatically.

I hope this clears things up. Let me know if you’ve run into the same confusion!
