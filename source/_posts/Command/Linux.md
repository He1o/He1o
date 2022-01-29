---
title: Linux
date: 2022-01-09
category: Command
---
<!--more-->
# Linux

## 网络

### 网络第一包慢
```bash
ping -n refclient.ext.here.com
```
>PING refclient.ext.here.com (108.139.1.24) 56(84) bytes of data.
>64 bytes from 108.139.1.24: icmp_seq=1 ttl=243 time=1.18 ms
>64 bytes from 108.139.1.24: icmp_seq=2 ttl=243 time=1.18 ms
>64 bytes from 108.139.1.24: icmp_seq=3 ttl=243 time=1.14 ms
>64 bytes from 108.139.1.24: icmp_seq=4 ttl=243 time=1.15 ms
>64 bytes from 108.139.1.24: icmp_seq=5 ttl=243 time=1.14 ms
>64 bytes from 108.139.1.24: icmp_seq=6 ttl=243 time=1.14 ms

```bash
time ping -n refclient.ext.here.com -c 1
```
>1 packets transmitted, 1 received, 0% packet loss, time 0ms
>rtt min/avg/max/mdev = 1.188/1.188/1.188/0.000 ms
>real    0m5.011s
>user    0m0.000s
>sys     0m0.000s