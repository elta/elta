---
layout: post
category: "Default"
description: "在 MacOS 上编译 QEMU 模拟器"
title:  "在 MacOS 上编译 QEMU"
date: 2017-02-21 17:10:38+00:00
tags: [qemu, macos]
---

在 Mac 上编译 QEMU 时，发现无法链接 pthread 库。经过搜索，在 stackoverflow 上找到了以下解决方法：

> clang requires -pthread when compiling but not when linking. This is annoying, but it is observed behavior:
>
> ```
>$ clang -c x.cpp
>$ clang -pthread -c x.cpp
>$ clang -o x x.o
>$ clang -pthread -o x x.o
>clang: warning: argument unused during compilation: '-pthread'
>$ 
>
>$ clang --version
>Apple LLVM version 5.0 (clang-500.2.76) (based on LLVM >3.3svn)
>Target: x86_64-apple-darwin13.0.0
>Thread model: posix
>```

既然知道了解决方法，那么做法也就简单了。

在命令行里为编译参数增加上 -lpthread 就可以了。

```
export CLFAGS+=" -lpthread "
```

之后进行编译，顺利通过。

参考文献：

[Stack Overflow](http://stackoverflow.com/questions/17841140/os-x-clang-pthread)