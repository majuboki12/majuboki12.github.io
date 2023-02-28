---
title : How to Configure Local Repository on RHEL 9.x
date : 2023-02-28 12:00:00 + 0900
categories : [Linux, RHEL]
tags : [rhel9, linux, repository, local, package, dnf, yum]
render_with_liquid: false
---

# 1. Mount RHEL 9.X Media and Copy Package file 

## 1.1 Mount RHEL 9.x media 

``` console 
# mount /dev/sr0 /mnt 
```

## 1.2 Create a local directory where the packages will be stored

```console
# mkdir -p /var/loacl/localrepo
```


## 1.3 Copy Package File 

```console 
# cp -rfpv /mnt/* /var/local/localrepo/ 
```


## 1.4 Umount rhel9.x media 
```console
# cd 
# umount /mnt 
```



# 2. Configuration yum repo files 


## 2.1 Back up your existing '.repo' file

```console 
# mkdir -p /etc/yum.repos.d/repo_bak
# mv /etc/yum.repos.d/*.repo /etc/yum.repos.d/repo_bak/
```


## 2.2 Create `local.repo` file 

`# vi /etc/yum.repos.d/local.repo`

```bash
[RHEL9.1_LocalRepository-BaseOS]
name=Redhat Enterprise Linux 9.1 - BaseOS
metadata_expire=-1
gpgcheck=0
enabled=1
baseurl=file:///var/local/localrepo/BaseOS
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-centosofficial

[RHEL9.1_LocalRepository-AppStream]
name=Redhat Enterprise Linux 9.1 - AppStream
metadata_expire=-1
gpgcheck=0
enabled=1
baseurl=file:///var/local/localrepo/AppStream
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-centosofficial
```

> 위에 .repo 파일은 vi를 사용하여 '/etc/yum.repos.d' 디렉토리 및에 작성을해도 되지만, 
 dnf config-manager command를 통하여 자동으로 생성할 수 있다.
{: .prompt-info } 





## 2.3 Package repository update 

```console 
# dnf repolist 

<Output Example> 
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

repo id                                         repo name
RHEL9.1_LocalRepository-AppStream               CentOS Linux 8 - AppStream
RHEL9.1_LocalRepository-BaseOS                  Redhat Enterprise Linux 9.1 - BaseOS
```


# 3. Verify Package List 

```console
# dnf list | grep -i localrepository | head -5

< Output Example > 
ModemManager-glib.x86_64                             1.18.2-3.el9                       @RHEL9.1_LocalRepository-BaseOS
abattis-cantarell-fonts.noarch                       0.301-4.el9                        @RHEL9.1_LocalRepository-AppStream
adobe-source-code-pro-fonts.noarch                   2.030.1.050-12.el9.1               @RHEL9.1_LocalRepository-AppStream
adwaita-cursor-theme.noarch                          40.1.1-3.el9                       @RHEL9.1_LocalRepository-AppStream
adwaita-icon-theme.noarch                            40.1.1-3.el9                       @RHEL9.1_LocalRepository-AppStream
```
