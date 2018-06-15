---
layout: post
category: "Default"
description: "Linux调试"
title:  "Linux bug 调试，关于网络协议和futext"
date: 2018-06-15 14:28:41+00:00
tags: [address_family,futext]
---

问题1，错误信息如下：

```
socket: address family not supported by protocol
```

解决方法：修改内核，在网络选项下，选上更多的协议

问题2，错误信息如下：

```
the futex facility returned an unexpected error code
``

解决方法：修改内核配置，增加futex的支持。