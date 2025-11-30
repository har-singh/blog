---
layout: post
title: Disable IPv6 on Debian
date: 2022-06-15 13:06
author: har-singh
comments: true
categories: [linux]
---

When running a lab VM, IPv6 is often not needed. Keeping things simple helps avoid unexpected issues.

## Check Current IPv6 Usage

```bash
sudo lsof -n | grep -i tcp
sshd       456    root    3u     IPv4    14117    0t0    TCP *:ssh (LISTEN)
sshd       456    root    4u     IPv6    14140    0t0    TCP *:ssh (LISTEN)
nginx     5536    root    6u     IPv4    23900    0t0    TCP *:http (LISTEN)
nginx     5536    root    7u     IPv6    23901    0t0    TCP *:http (LISTEN)
```

## Method 1: sysctl.conf (Recommended)

```bash
# Edit /etc/sysctl.conf
sudo vi /etc/sysctl.conf

# Add these lines at the bottom
net.ipv6.conf.all.disable_ipv6=1
net.ipv6.conf.default.disable_ipv6=1
net.ipv6.conf.lo.disable_ipv6=1

# Apply changes
sudo sysctl -p
```

## Method 2: GRUB

```bash
# Edit /etc/default/grub
sudo vi /etc/default/grub

# Change these lines
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash ipv6.disable=1"
GRUB_CMDLINE_LINUX="ipv6.disable=1"

# Update GRUB and reboot
sudo update-grub
sudo reboot
```

Source: [BLOG-D](https://dannyda.com/2021/06/10/how-to-disable-ipv6-in-linux-debian-ubuntu-kali-linux-centos-8-rhel-8-fedora-etc/)

---

## Fixing Nginx After Disabling IPv6

After disabling IPv6, nginx may fail to start:

```
nginx: [emerg] socket() [::]:80 failed (97: Address family not supported by protocol)
```

**Solution:** Edit nginx config to listen on IPv4 only:

```bash
# Edit nginx config
sudo vim /etc/nginx/sites-enabled/default

# Comment out this line:
# listen [::]:80 default_server;

# Restart nginx
sudo systemctl restart nginx
```

After the fix:

```bash
sudo lsof -n | grep -i tcp
sshd      460    root    3u     IPv4    13874    0t0    TCP *:ssh (LISTEN)
nginx     589    root    6u     IPv4    16525    0t0    TCP *:http (LISTEN)
```

Source: [techglimpse.com](https://techglimpse.com/nginx-error-address-family-solution/)
