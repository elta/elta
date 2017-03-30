---
layout: post
category: "linux"
description: "Linux 内核配置 —— DEVTMPFS，自动产生 /dev 目录下设备"
title:  "Linux 内核配置 —— DEVTMPFS"
date: 2017-03-30 09:29:12+00:00
tags: [linux，config]
---

在 Linux 内核配置完成后，建立 ROOTFS 时，/dev 目录下的设备信息可以手动创建，但是也可以通过内核来自动产生。

自动产生 /dev 目录下设备的方法，是在内核配置过程中，加入对 DEVTMPFS 的选择。

```
> linux-4.10

CONFIG_DEVTMPFS:

 This creates a tmpfs/ramfs filesystem instance early at bootup. 
 In this filesystem, the kernel driver core maintains device 
 nodes with their default names and permissions for all
 registered devices with an assigned major/minor number. 
 Userspace can modify the filesystem content as needed, add
 symlinks, and apply needed permissions. 
 It provides a fully functional /dev directory, where usually
 udev runs on top, managing permissions and adding meaningful
 symlinks. 
 In very limited environments, it may provide a sufficient 
 functional /dev without any further help. It also allows simple 
 rescue systems, and reliably handles dynamic major/minor numbers. 
 
 Notice: if CONFIG_TMPFS isn't enabled, the simpler ramfs
 file system will be used instead. 
 
 Symbol: DEVTMPFS [=y] 
 Type  : boolean 
 Prompt: Maintain a devtmpfs filesystem to mount at /dev 
   Location: 
     -> Device Drivers 
       -> Generic Driver Options 
   Defined at drivers/base/Kconfig:2


```