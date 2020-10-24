---
layout: composer报错 Cannot allocate memory
title: memory
date: 2020-08-27 14:42:16
tags:
---
```
sudo /bin/dd if=/dev/zero of=/var/swap.1 bs=1M count=1024&&sudo /sbin/mkswap /var/swap.1&&sudo /sbin/swapon /var/swap.1

```