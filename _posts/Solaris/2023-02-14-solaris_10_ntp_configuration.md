---
title : How to Configure NTP Client on Solaris 5.10 
date : 2023-02-14 14:00:00 + 0900
categories : [SERVER, UNIX]
tags : [oracle, solaris, ntp, client]
render_with_liquid: false
---

# How to Configure NTP Client on Solaris 5.10 


## 1. `ntp.conf` 파일 생성 
```
# cp /etc/inet/ntp.client /etc/inet/ntp.conf
```


## 2. `ntp.conf` 파일에 NTP server list 추가 

`modify` /etc/inet/ntp.conf
```bash
# ident "@(#)ntp.client 1.3     00/07/17 SMI"
#
# /etc/inet/ntp.client
#
# An example file that could be copied over to /etc/inet/ntp.conf; it
# provides a configuration for a host that passively waits for a server
# to provide NTP packets on the ntp multicast net.
#

#multicastclient 224.0.1.1		## 주석처리 

server  216.239.35.8 prefer		# NTP 서버 time.google.com Primary 
server  216.239.35.4			# NTP 서버 time.google.com Secondary 
```


## 3. NTP 서비스 재시작 
```
# svcadm disable svc:/network/ntp:default 
```

## 4. NTP 서비스 상태 및 동기화 확인 

### 4.1 NTP 서비스 상태 확인 
```
# svcs -l  svc:/network/ntp:default
fmri         svc:/network/ntp:default
name         Network Time Protocol (NTP)
enabled      true
state        online
next_state   none
state_time   Tue Feb 14 14:15:46 2023
logfile      /var/svc/log/network-ntp:default.log
restarter    svc:/system/svc/restarter:default
contract_id  1582
dependency   require_all/error file://localhost/usr/sbin/ntpq (online) file://localhost/usr/sbin/ntpdate (online)
dependency   require_any/error svc:/network/service (online)
dependency   optional_all/error svc:/milestone/name-services (online)
dependency   require_all/error svc:/system/filesystem/minimal (online)
```

### 4.2 시간 동기화 확인 

NTP 서버와의 동기화 확인
```
# ntpq -p 
     remote           refid      st t when poll reach   delay   offset    disp
==============================================================================
*216.239.35.8    .GOOG.           1 u   35   64  377    47.44   -0.768    1.11
+216.239.35.4    .GOOG.           1 u   34   64  377    54.89    3.327    0.79
```

시간 확인
```
# date
Tue Feb 14 14:18:11 KST 2023
```