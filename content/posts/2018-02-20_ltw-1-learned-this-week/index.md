---
title: "LtW 1 — Learned this Week"
author: "Jordi Coscolla"
date: 2018-02-20T10:25:36.557Z
lastmod: 2020-02-11T21:51:05+01:00

description: ""

subtitle: "ADB keys"

image: "/posts/2018-02-20_ltw-1-learned-this-week/images/1.png" 
images:
 - "/posts/2018-02-20_ltw-1-learned-this-week/images/1.png" 


aliases:
    - "/ltw-1-learned-this-week-c026eb999840"
---

### ADB keys

Android uses adb to comunicate you computer with the device, and for authenticating the comunication it uses RSA keys in the same fashion as SSH.

When you connect the device to your computer in Development mode a nice “allow this computer” alert appears. After you accept your public key of adb (located at $HOME/.android/adbkey.pub) will be copied into the device as an authorized computer.

When building AOSP you can add your own public key at /adb_keys or /data/misc/adb_keys and never be asked to use adb.

### Jenkins + Docker + Windows 10

Jenkins plugin for docker is awesome, but… it’s only thought for using with linux… on windows I found no way to make it work.

The docker command tries to mount the git source folder that is let’s say C:\jenkins\workspace to inside the container to C:\jenkins\workspace but since the container is linux based it complains that can not mount it… at the end I had to use another aproach :(

### Ikigai

Japanese have words that impress…




![image](/posts/2018-02-20_ltw-1-learned-this-week/images/1.png)
