---
title : How to Install OpenJDK 1.8 on RHEL 9.x (Using dnf) 
date : 2023-02-28 13:00:00 + 0900
categories : [Linux, RHEL]
tags : [rhel9, openjdk, install, dnf] 
render_with_liquid: false
---

# 1. Open JDK Package List 확인
설치하려는 OS의 Package repository에 설치 가능한 JDK 버전 확인. 
본 문서에서는 RHEL 9.1 버전의 설치 media를 통해 local repository 구성 후 jdk 설치를 진행. 

local repository 구성 방법은 아래 링크 참고 ↓
<http://majuboki12.github.io/posts/how_to_config_RHEL_9_X_local_repository/> 


```console 
# dnf list | grep -i "java-"
java-1.8.0-openjdk.x86_64                            1:1.8.0.345.b01-5.el9              RHEL9.1_LocalRepository-AppStream
java-1.8.0-openjdk-demo.x86_64                       1:1.8.0.345.b01-5.el9              RHEL9.1_LocalRepository-AppStream
java-1.8.0-openjdk-devel.x86_64                      1:1.8.0.345.b01-5.el9              RHEL9.1_LocalRepository-AppStream
java-1.8.0-openjdk-headless.x86_64                   1:1.8.0.345.b01-5.el9              RHEL9.1_LocalRepository-AppStream
java-1.8.0-openjdk-javadoc.noarch                    1:1.8.0.345.b01-5.el9              RHEL9.1_LocalRepository-AppStream
java-1.8.0-openjdk-javadoc-zip.noarch                1:1.8.0.345.b01-5.el9              RHEL9.1_LocalRepository-AppStream
java-1.8.0-openjdk-src.x86_64                        1:1.8.0.345.b01-5.el9              RHEL9.1_LocalRepository-AppStream
java-11-openjdk.x86_64                               1:11.0.16.1.1-3.el9                RHEL9.1_LocalRepository-AppStream

 . . . 
 
```  
해당 문서에서는 `java-1.8.0-openjdk`를 설치 함. 



# 2. Open JDK 1.8 Installation 
```console 
# dnf install -y java-1.8.0-openjdk*
```



# 3. Modify alternatives 

**alternatives list 확인**

```console 
# alternatives --list

< Outpu Example >
libnssckbi.so.x86_64    auto    /usr/lib64/pkcs11/p11-kit-trust.so
soelim                  auto    /usr/bin/soelim.groff
iptables                auto    /usr/sbin/iptables-nft
ebtables                auto    /usr/sbin/ebtables-nft
arptables               auto    /usr/sbin/arptables-nft
cifs-idmap-plugin       auto    /usr/lib64/cifs-utils/cifs_idmap_sss.so
man                     auto    /usr/bin/man.man-db
java                    auto    /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64/jre/bin/java
jre_openjdk             auto    /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64/jre
jre_1.8.0               auto    /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64/jre
jre_1.8.0_openjdk       auto    /usr/lib/jvm/jre-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64
javac                   auto    /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64/bin/javac
java_sdk_openjdk        auto    /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64
java_sdk_1.8.0          auto    /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64
java_sdk_1.8.0_openjdk  auto    /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64
javadocdir              auto    /usr/share/javadoc/java-1.8.0-openjdk-1.8.0.345.b01-5.el9/api
javadoczip              auto    /usr/share/javadoc/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.zi
```


**불필요한 alternatives(symbolic) list를 제거**

```console
# alternatives --remove java_sdk_openjdk /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64/jre
# alternatives --remove jre_openjdk /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64/jre
# alternatives --remove jre_1.8.0 /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64/jre
# alternatives --remove jre_1.8.0_openjdk /usr/lib/jvm/jre-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64 
# alternatives --remove javac /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64/bin/javac
# alternatives --remove java_sdk_openjdk /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64 
# alternatives --remove java_sdk_1.8.0 /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64
# alternatives --remove java_sdk_1.8.0_openjdk /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64
# alternatives --remove javadocdir /usr/share/javadoc/java-1.8.0-openjdk-1.8.0.345.b01-5.el9/api
# alternatives --remove javadoczip /usr/share/javadoc/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.zip
```


**불필요한 list들이 제거되었는지 확인**
```console 
# alternatives --list
libnssckbi.so.x86_64    auto    /usr/lib64/pkcs11/p11-kit-trust.so
soelim                  auto    /usr/bin/soelim.groff
iptables                auto    /usr/sbin/iptables-nft
ebtables                auto    /usr/sbin/ebtables-nft
arptables               auto    /usr/sbin/arptables-nft
cifs-idmap-plugin       auto    /usr/lib64/cifs-utils/cifs_idmap_sss.so
man                     auto    /usr/bin/man.man-db
java                    manual  /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64/jre/bin/java
```


# 3. JDK 설치 확인


**Symbolic 확인** 
```console
# alternatives --config java

There is 1 program that provides 'java'.

  Selection    Command
-----------------------------------------------
*+ 1           java-1.8.0-openjdk.x86_64 (/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.345.b01-5.el9.x86_64/jre/bin/java)
```


**Java Verison 확인**
```console 
# java -version
openjdk version "1.8.0_345"
OpenJDK Runtime Environment (build 1.8.0_345-b01)
OpenJDK 64-Bit Server VM (build 25.345-b01, mixed mode)
```




