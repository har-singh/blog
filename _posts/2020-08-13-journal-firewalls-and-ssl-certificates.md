---
layout: post
title: "Journal: Exploring Firewalls and SSL Certificates"
date: 2020-08-13 10:23
author: har-singh
comments: true
categories: [journal]
---

Looking at Let’s Encrypt SSL certificate options:

  - Let’s Encrypt Certificates on GoDaddy Hosting - [letsencrypt.org](https://letsencrypt.org/docs/godaddy/)
  - Install a Let’s Encrypt certificate on your Linux Hosting account- [godaddy.com](https://uk.godaddy.com/help/install-a-lets-encrypt-certificate-on-your-linux-hosting-account-28023)
  - How to change your DNS settings in GoDaddy- [rocketspark.com](https://support.rocketspark.com/hc/en-us/articles/115010277387-How-to-change-your-DNS-settings-in-GoDaddy)
  - Let’s Encrypt Getting Started – Manual Mode- [certbot.eff.org]](https://certbot.eff.org/docs/using.html#manual)

Discovered that GoDaddy’s cPanel provides built-in email support with up to 100 accounts.

**Technical Notes:**
For SSL certificates, I needed to update the DNS hosts file hosted on GoDaddy servers for the domain. This was a good opportunity to better understand DNS systems, especially after discussing DNS steering in a recent technical interview.

Watched videos to deepen my understanding of DNS SOA, Name Servers, and the history of DNS. The videos helped clarify the importance of these concepts in the broader context of networking.

- Nameservers in DNS – What are… - [youtube.com](https://www.youtube.com/watch?v=KY7I18OCMwY)
- 25 Years of DNS - [youtube.com](https://www.youtube.com/watch?v=Rw96pH_Kdxo)

Set Up a DNS Name Server - [wired.com](https://www.wired.com/2010/02/set_up_a_dns_name_server/)

### Structure of Domain Names

*Domain name data is structured hierarchically. At the top level is the root node. Every domain on the Internet is a member of the root node. Under the root node are top-level domains like `.com`, `.edu`, `.org`, `.uk`, `.ru`, `.biz`, etc. Below that are domain names such as `webmonkey.com`, `navy.mil`, or country code extensions like `.co.uk`. Anything beneath that is a subdomain or host. Subdomain names can be layered to a total depth of 127 levels.*

How To Use Nslookup To Check DNS TXT Record - [rmilne.ca](https://blog.rmilne.ca/2015/09/11/how-to-use-nslookup-to-check-dns-txt-record/)
