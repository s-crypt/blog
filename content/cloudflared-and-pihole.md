---
title: The Better Way to use cloudflared and PiHole
date: 2024-04-26
tags:
  - information
  - technology
---
## The [current documented way](https://web.archive.org/web/20240427053050/https://docs.pi-hole.net/guides/dns/cloudflared/) sucks.
It is bloated with many unnecessary instructions. If all you want to do is use cloudflared to forward your DNS requests securely to the provider of your choice, it is actually quite simple. Just add install via the repo, create the service, and enable it.

### 1. Install cloudflared
Go to [pkg.cloudflare.com](https://pkg.cloudflare.com/index.html) and add the repository to your distribution following their directions. This way it updates with apt.

### 2. Create the service configuration
You want to create a configuration that tells the automatic service how to run.
Create the file using `sudo nano /etc/systemd/system/cloudflared-proxy-dns.service`
and paste in the following information:
```systemd
[Unit]
Description=DNS over HTTPS (DoH) proxy client
Wants=network-online.target nss-lookup.target
Before=nss-lookup.target

[Service]
AmbientCapabilities=CAP_NET_BIND_SERVICE
CapabilityBoundingSet=CAP_NET_BIND_SERVICE
DynamicUser=yes
ExecStart=/usr/local/bin/cloudflared proxy-dns --port 5053 --upstream 

[Install]
WantedBy=multi-user.target
```

after `--port 5053 --upstream`, paste the URL of the DNS-over-HTTPS endpoint you want to use, like `https://dns.nextdns.io/123abc`.

### 3. Enable the service
Run `sudo systemctl enable --now cloudflared-proxy-dns`

### 4. Change the DNS in PiHole
Change the DNS server in settings so that the only server is `127.0.0.1#5053`

**That's it.**
You don't need extra users and permissions or another binary you will forget to update. This will auto run on system startup and update with the rest of the OS and packages.