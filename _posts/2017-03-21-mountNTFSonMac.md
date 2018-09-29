---
layout: post
category: "mac"
description: "在 Mac 上挂载 NTFS 格式的磁盘"
title:  "在 Mac 上挂载 NTFS 格式的磁盘"
date: 2017-03-21 15:38:38+00:00
tags: [mac,ntfs]
---

在 Mac 上默认的 NTFS 格式磁盘是只读的，为了让磁盘能够进行写入，需要手动执行命令。

具体命令如下：

```
mkdir -pv ./udisk
sudo mount -t ntfs -o nobrowse,rw /dev/disk3s1 ./udisk/
```

通过上述命令，首先创建了一个叫 udisk 的文件夹，然后将 NTFS 格式的磁盘挂载到 udisk 上。

我的磁盘是 /dev/disk3s1，在进行挂载时，需要根据实际情况选择磁盘进行挂载。查找磁盘名称的方式有两种，通过 diskutil 和 mount。

## 通过 diskutil 查看磁盘

通过 diskutil 查看，通过执行

```
diskutil list
```

查看执行结果，确认对应的磁盘位置。

## 通过 mount 查看磁盘

因为系统会自动挂载磁盘，所以在系统挂载上磁盘后，我们可以通过执行 mount 命令，查看每一个磁盘和磁盘的挂载点。确认了磁盘位置后，先执行 umount 命令取消磁盘挂载，然后再用上面的 mount 命令进行读取权限的挂载。
