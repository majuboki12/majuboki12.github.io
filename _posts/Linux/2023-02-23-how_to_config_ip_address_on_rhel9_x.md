---
title : How to Configure Network in RHEL 9.x (Using CLI) 
date : 2023-02-23 21:00:00 + 0900
categories : [Linux, RHEL]
tags : [rhel9, linux, netowork, ipv4, ipv6, nmcli] 
render_with_liquid: false
---

# 1. IP 설정 정보  

| ITEMS | CONFIG |
|:---|:---|   
| Connection Name | public-network | 
| Static IPv4 Address / Subnet mask | 192.168.150.182/24 | 
| Static IPv6 Address / Subnet mask | Disabled |
| IPv4 Default Gateway | 192.168.150.1 |
| IPv4 DNS Server | 8.8.8.8 | 
| DNS Search Domain | google.com | 



# 2. 설정할 Network Device List 확인 

``` console
# nmcli device show

< Output Example >  
GENERAL.DEVICE:                         ens192
GENERAL.TYPE:                           ethernet
. . . 

GENERAL.DEVICE:                         lo
GENERAL.TYPE:                           loopback
. . . 
``` 


# 3. Network Configuration 

## 3.1 Add Connection Name 

``` console 
# nmcli connection add  con-name public-network ifname ens192 type ethernet 
```  
  
  
  
`설정 정보 확인` 

```console 
# nmcli -g connection.type,connection.interface-name connection show public-network

<Output Example> 
802-3-ethernet
ens192
```

<br>

> nmcli 사용법에 대해 더 자세한 내용을 확인하고 싶으면, `man nmcli-examples`
또는, `nmcli --help` command를 입력하여 확인할 수 있다.
{: .prompt-info } 

<br>

## 3.2 Set IPv4 Address and Gateway,  IPv4 Method to Manual 

```console 
< Set IPv4 IP Address > 
# nmcli connection modidfy public-network ipv4.addresses 192.168.150.182/24 

< Set IPv4 IP Gateway 
# nmcli connection modify public-network ipv4.gateway 192.168.150.1 

  
<Set IPv4 Method to Manual> 
# nmcli connection modify public-network ipv4.method manual 
```
    
`설정 정보 확인`  

```console 
# nmcli -g ipv4.addresses,ipv4.gateway,ipv4.method connection show public-network
             

< Output Example> 
192.168.150.182/24		# IPv4 Address 
192.168.150.1			# IPv4 Gateway 
manual				# IPv4 Method ( Auto or Manual ) 
```

## 3.3 DNS Server Configuration 

```console 
< Set IPv4 DNS Server > 
# nmcli connection modify public-network ipv4.dns "8.8.8.8"

< Set IPv4 DNS-search > 
# nmcli connection modify public-network ipv4.dns-search google.com 
```

`설정 정보 확인` 

```console 
# nmcli -g ipv4.dns,ipv4.dns-search connection show public-network

<Output Example> 
8.8.8.8			# IPv4 DNS Server 
google.com		# IPv4 dns-search 
``` 


# 4. Set IPv6 Disable 

```console 
# nmcli connection modify public-network ipv6.method disabled
```` 


`설정 정보 확인` 

```console 
# nmcli -g ipv6 connection show public-network

<Output Example>
ipv6:disabled::::0::::-1:0::no:no:no:yes:-1:-1:default:0:auto:::0:yes::0x0:
```


# 5. Bring up 'public-network' 

```console 
# nmcli connection up public-network
``` 


# 6. Verifying Network 

```console 
# nmcli 

<Output Example> 
ens192: connected to public-network
        "VMware VMXNET3"
        ethernet (vmxnet3), 00:50:56:A1:28:53, hw, mtu 1500
        ip4 default
        inet4 192.168.150.182/24
        route4 192.168.150.0/24 metric 100
        route4 default via 192.168.150.1 metric 100

lo: unmanaged
        "lo"
        loopback (unknown), 00:00:00:00:00:00, sw, mtu 65536

DNS configuration:
        servers: 8.8.8.8
        domains: google.com
        interface: ens192
```


