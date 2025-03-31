---
layout: post
title: Disable IPv6 on Debian
date: 2022-06-15 13:06
author: har-singh
comments: true
categories: [bash, ipv6]
---
<!-- wp:paragraph -->
<p>When running lab vm the IPv6 is not needed. It is good to keep things simple.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"bash"} -->
<pre class="wp-block-syntaxhighlighter-code"># List of files with tcp filter
geek@debian:~$ sudo lsof -n | grep -i tcp
sshd       456                           root    3u     IPv4              14117      0t0        TCP *:ssh (LISTEN)
sshd       456                           root    4u     IPv6              14140      0t0        TCP *:ssh (LISTEN)
nginx     5536                           root    6u     IPv4              23900      0t0        TCP *:http (LISTEN)
nginx     5536                           root    7u     IPv6              23901      0t0        TCP *:http (LISTEN)
nginx     5539                       www-data    6u     IPv4              23900      0t0        TCP *:http (LISTEN)
nginx     5539                       www-data    7u     IPv6              23901      0t0        TCP *:http (LISTEN)</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:heading -->
<h2>Two methods</h2>
<!-- /wp:heading -->

<!-- wp:syntaxhighlighter/code {"language":"bash"} -->
<pre class="wp-block-syntaxhighlighter-code"># Method 1 – /etc/sysctl.conf

# Edit /etc/sysctl.conf file
sudo vi /etc/sysctl.conf

# Add following lines at the bottom of the file
net.ipv6.conf.all.disable_ipv6=1
net.ipv6.conf.default.disable_ipv6=1
net.ipv6.conf.lo.disable_ipv6=1
# :wq, Enter key to Exist and Save the file

# Apply the changes
sudo sysctl -p</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:paragraph -->
<p>or</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"bash"} -->
<pre class="wp-block-syntaxhighlighter-code"># Method 2 – GRUB
# Edit the /etc/default/grub file
sudo vi /etc/default/grub

# Find the following lines
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
GRUB_CMDLINE_LINUX=""

# Change to
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash ipv6.disable=1"
GRUB_CMDLINE_LINUX="ipv6.disable=1"

# Update GRUB
sudo update-grub

# Restart the system
sudo reboot</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:paragraph -->
<p>Source: <a href="https://dannyda.com/2021/06/10/how-to-disable-ipv6-in-linux-debian-ubuntu-kali-linux-centos-8-rhel-8-fedora-etc/" target="_blank" rel="noreferrer noopener">BLOG-D</a></p>
<!-- /wp:paragraph -->

<!-- wp:separator -->
<hr class="wp-block-separator has-alpha-channel-opacity" />
<!-- /wp:separator -->

<!-- wp:paragraph -->
<p>After the reboot nginx was not working</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>geek@debian:~$ sudo systemctl status nginx
<mark style="background-color:rgba(0, 0, 0, 0);color:#e10000;" class="has-inline-color">●</mark> nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: <mark style="background-color:rgba(0, 0, 0, 0);color:#da0000;" class="has-inline-color">failed </mark>(Result: exit-code) since Wed 2022-06-15 12:42:23 BST; 41s ago
       Docs: man:nginx(8)
    Process: 434 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (<mark style="background-color:rgba(0, 0, 0, 0);color:#da0000;" class="has-inline-color">code=exited, status=1/FAILURE</mark>)
        CPU: 32ms

Jun 15 12:42:23 debian systemd&#091;1]: Starting A high performance web server and a reverse proxy server...
Jun 15 12:42:23 debian nginx&#091;434]: nginx: &#091;emerg] socket() &#091;::]:80 failed (97: Address family not supported by protocol)
Jun 15 12:42:23 debian nginx&#091;434]: nginx: configuration file /etc/nginx/nginx.conf test failed
Jun 15 12:42:23 debian systemd&#091;1]: nginx.service: Control process exited, code=exited, status=1/FAILURE
Jun 15 12:42:23 debian systemd&#091;1]: <mark style="background-color:rgba(0, 0, 0, 0);color:#e7dd0d;" class="has-inline-color">nginx.service: Failed with result 'exit-code'.</mark>
Jun 15 12:42:23 debian systemd&#091;1]: <mark style="background-color:rgba(0, 0, 0, 0);color:#da0000;" class="has-inline-color">Failed to start A high performance web server and a reverse proxy server.</mark></code></pre>
<!-- /wp:code -->

<!-- wp:separator -->
<hr class="wp-block-separator has-alpha-channel-opacity" />
<!-- /wp:separator -->

<!-- wp:paragraph -->
<p><strong>How to fix Nginx error: Address family not supported by protocol</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Solution: The error message indicates that the service is trying to start on IPv6 address “[::]:80” and failed due to unsupported address family. It means, the machine does not have an IPv6 address set. All you need to do is, simply edit the Ngnix configuration file to listen on IPv4 address as shown below.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="https://techglimpse.com/nginx-error-address-family-solution/" target="_blank" rel="noreferrer noopener">techglimpse.com</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code {"language":"bash"} -->
<pre class="wp-block-syntaxhighlighter-code"># Step 1: Open /etc/nginx/sites-enabled/default
vim /etc/nginx/sites-enabled/default

# Step 2: Comment the below line:
listen [::]:80 default_server;

# Now restart the nginx service and it should work.</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:code -->
<pre class="wp-block-code"><code>geek@debian:/etc/nginx$ sudo systemctl status nginx
<mark style="background-color:rgba(0, 0, 0, 0);color:#47d504;" class="has-inline-color">●</mark> nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: <mark style="background-color:rgba(0, 0, 0, 0);color:#47d504;" class="has-inline-color">active (running)</mark> since Wed 2022-06-15 12:45:23 BST; 6s ago
       Docs: man:nginx(8)
    Process: 587 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
    Process: 588 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
   Main PID: 589 (nginx)
      Tasks: 2 (limit: 2301)
     Memory: 2.5M
        CPU: 21ms
     CGroup: /system.slice/nginx.service
             ├─589 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
             └─590 nginx: worker process

Jun 15 12:45:23 debian systemd&#091;1]: Starting A high performance web server and a reverse proxy server...
Jun 15 12:45:23 debian systemd&#091;1]: nginx.service: Failed to parse PID from file /run/nginx.pid: Invalid argument
Jun 15 12:45:23 debian systemd&#091;1]: Started A high performance web server and a reverse proxy server.</code></pre>
<!-- /wp:code -->

<!-- wp:separator -->
<hr class="wp-block-separator has-alpha-channel-opacity" />
<!-- /wp:separator -->

<!-- wp:syntaxhighlighter/code {"language":"bash"} -->
<pre class="wp-block-syntaxhighlighter-code">geek@debian:/etc/nginx$ sudo lsof -n | grep -i tcp
sshd      460                           root    3u     IPv4              13874      0t0        TCP *:ssh (LISTEN)
sshd      486                           root    4u     IPv4              nginx     589                           root    6u     IPv4              16525      0t0        TCP *:http (LISTEN)
nginx     590                       www-data    6u     IPv4              16525      0t0        TCP *:http (LISTEN)
</pre>
<!-- /wp:syntaxhighlighter/code -->
