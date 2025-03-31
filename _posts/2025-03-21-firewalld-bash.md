---
layout: post
title: Firewall Management with firewalld
date: 2025-03-21 17:48
author: har-singh
comments: true
categories: [bash]
---

Firewall Management with firewalld

## 1. Check if `firewalld` is Running
To check if `firewalld` is active:

```bash
sudo systemctl status firewalld
```

Alternatively, check its state:

```bash
sudo firewall-cmd --state
```

## 2. View Active Rules
To view all active firewall rules:

```bash
sudo firewall-cmd --list-all
```

To see allowed services:

```bash
sudo firewall-cmd --list-services
```

## 3. Services vs. Rich Rules

- **Services**: Predefined configurations that open standard ports. For example, the `http` service opens TCP port 80.
- **Rich Rules**: Custom, granular rules allowing more specific configurations (e.g., blocking specific IPs or logging).

### Key Point:
- If there’s **no rich rule for port 80**, the `http` service will allow traffic on port 80.

## 4. Troubleshooting
- If a service is listed but not working, check for conflicting rich rules that may block the traffic.
- If `firewalld` isn’t running, start it with:

```bash
sudo systemctl start firewalld
```

*Note: Post finalized using LLMs (chatgpt)*
