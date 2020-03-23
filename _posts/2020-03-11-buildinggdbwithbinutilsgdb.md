---
layout: post
category: "Default"
description: ""
title:  "使用binutils-gdb来编译gdb和binutils"
date: 2020-03-11 19:57:11+00:00
tags: [Default]
---

gdb 和 binutils 是两个独立的项目，但是他们的 git 仓库却是同一个。

当下载完成后，会发现在源码中同时包含了 gdb 的目录和 binutils 各个工具的源码目录。为了实现 gdb 或 binutils 的独立编译，需要指定编译的工具。

# 编译 GDB

编译 GDB 的参数如下：

```
../binutils-gdb/configure --disable-binutils --disable-ld \
    --disable-gold --disable-gas --disable-sim --disable-gprof
```

添加 CFLAGS 进行编译的参数如下：

```
../binutils-gdb/configure --disable-binutils --disable-ld \
    --disable-gold --disable-gas --disable-sim --disable-gprof \
    CXXFLAGS='-g3 -O0' CFLAGS='-g3 -O0'
```

# 编译 BINUTILS

编译 binutils 则与编译 gdb 正好相反，直接 disable 掉 gdb 即可。

编译参数如下：

```
../configure --prefix=${PWD}/_install --disable-gdb
```

# 打包Release

## Release GDB

```
src-release.sh gdb
```

## Release Binutils

```
src-release.sh binutils
```

## 其它

```
src-release.sh [ binutils | gas | gdb | sim ]
```
