---
layout: post
category: "Default"
description: ""
title:  "关于物体 '固有类别' 与 '实际使用类别' 分离的情况，结构体定义方法"
date: 2017-05-22 10:47:57+00:00
tags: [Default]
---

在面向接口、面向对象编程的过程中，会遇到实际物体类别与定义类别相分离的情况。

例如，我们有三种物体，他们的固有类别分别为： TYPEA，TYPEB，TYPEC。在我们实际使用过程中，我们会根据不同的情况将他们分成 2 组： Group1，Group2。

那么，我们在定义结构体和物理类别时，需要注意对 Group 进行定义。定义物体具体属性和结构体如下：

```
#define TYPEA (0x01UL << 0)
#define TYPEB (0x01UL << 1)
#define TYPEC (0x01UL << 2)

typedef struct foo_t {
   ...
   uint64_t group1;
   uint64_t group2;
   ...
} foo_t;
```

在定义具体类型时，我们可以进行具体物体分类的实现：

```
foo_t fooA = {
    .group1 = TYPEA | TYPEB;
    .group2 = TYPEC;
};

foo_t fooB = {
    .group1 = TYPEA;
    .group2 = TYPEB | TYPEC;
};

uint64_t thingA = TYPEA;
uint64_t thignB = TYPEB;
```

通过定义，我们实现了两种具体的分类方式，fooA 和 fooB，并且实现了具体分组和物品类型的关联。并且，我们定义了两个具体的事物，thingA 和 thingB。

在实际编程过程中，我们对 thing 的判断方式如下：

```
uint64_t thingX = ...;

if (thingX & fooA.group1) {
    printf("ThingX insert into A.group1\n");
} else if (thingX & fooA.group2) {
    printf("ThingX insert into A.group2\n");
}
```

在具体代码使用过程中，我们不必再关心物品的固有类型，以及分组的类型。当需要修改分组类型时，我们只需要修改 group 定义时的类型，就能够实现类型的变更。

通过分组的抽象，与对抽象结果的使用，可以减少后期代码维护时的工作量。

当我们需要检测分析信息时，我们可以通过使用实际的类型，进行检测：

```
if (fooA.group1 & TYPEA) {
    printf("A.group1 contains TYPEA");
}
if (fooA.group1 & TYPEB) {
    printf("A.group1 contains TYPEB");
}
if (fooA.group1 & TYPEC) {
    printf("A.group1 contains TYPEC");
}


if (thingX & TYPEA) {
    printf("thingX belong to TYPEA");
} else if (thingX & TYPEB) {
    printf("thingX belong to TYPEB");
} else if (thingX & TYPEC) {
    printf("thingX belong to TYPEC");
}
```

在开发后期，可能会出现新的分类方式，对原有类型进行了分离。例如：TYPEA 分离成 TYPED 和 TYPEF，修改信息如下：

```
#define TYPED (0x01UL << 4)
#define TYPEF (0x01UL << 5)
#define TYPEA (TYPED | TYPEF)
```

通过对 TYPEA 的分离，原有 TYPEA 的逻辑并不需要进行更新，TYPED 和 TYPEF 相关的新逻辑添加就可以了。

这种情况下，原有类型 fooA 相关代码不需要进行更新，而新类型 fooX 可以添加 TYPED 和 TYPEF 的操作。