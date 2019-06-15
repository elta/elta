---
layout: post
category: "mac"
description: ""
title:  "在MacOS上利用docker构建buildroot"
date: 2019-06-13 15:46:22+00:00
tags: [mac,buildroot]
---

之前有听说过docker，但是一直没有使用过。最近终于下定决定使用了一下docker，感觉docker用于跨操作系统的软件工具使用还是比较友好的。

# 适用人群

本文忽略的部分Linux软件包安装的过程，需要读者有一定Linux操作基础，具有软件包查找与安装能力。

# Docker的基本用法

在使用docker时，首先需要安装docker。安装完成后，通过从dockerhub上下载不同系统环境的image，然后运行相应的image，完成docker的运行操作。

在docker的运行的过程，是通过docker命令调用image进行的运行，image运行的实体叫做container。image和container的关系比较像网吧系统的关系，网吧系统开机会加载操作系统，并且用户可以在操作系统中进行操作和修改；当系统关机重启后，再次开机的系统不会保留用户的更改，会还原成原本最初的系统状态。docker的过程与之相同，在docker使用image启动的container中，用户在container所做的操作并不会保存下来，而是会在用户退出的时候清除。

如果用户希望保存下container中的修改，则需要将container保存成一个新的image，实现对修改的保存；或者使用共享磁盘的形式，将外部系统的目录共享到container内部，共享磁盘上的修改会被保留。

## 从Docker Hub上下载image

docker官方提供了image的下载渠道dockerhub，地址为：https://hub.docker.com。

以Ubuntu为例，在dockerhub上，可以找到Ubuntu的image下载页面【https://hub.docker.com/_/ubuntu】，在该页面中可以看到很多不同的Ubuntu的版本信息，通过

```
docker pull ubuntu
```

可以完成对Ubuntu最新image的下载，也可以通过tag页面中根据tag寻找到所需的image，对指定的image进行下载。例如下载Ubuntu 1804的image，命令如下：

```
docker pull ubuntu:18.04
```

下载完成后，本地通过docker images命令可以看到所下载的镜像了。

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              18.04               7698f282e524        4 weeks ago         69.9MB
```

由于这个镜像只是一个最小的系统环境，包含了软件包安装命令apt，所以这个镜像很小。如果后续需要装更多的软件包，并且创建新的image，新的image的尺寸会变大。

## 运行image

使用docker运行image的命令如下：

```
docker run ubuntu:18.04 bash
```

上面的命令是通过docker调用了ubuntu:18.04image中的bash。但是该命令一闪而过，没有留下任何痕迹。这并不是运行错误，而是因为bash运行完成之后退出了。如果不希望运行后退出，而是留在终端里，可以通过下述命令来进行执行：

```
docker run -it ubuntu:18.04
```

上述命令运行完成后，可以停留在shell中，该shell是docker所运行的Ubuntu image的container的shell，可以看到命令提示如下：

```
root@7ab5341e698c:/# 
```

进入container后，用户为root，容器编号为7ab5341e698c，停留的目录为“/”。接下来，就可以在容器内进行各种操作了，可以通过apt命令去安装自己所需的软件。

**注意**

退出容器时，如果直接使用exit命令会导致容器退出，所有容器内部的更改将会丢失。如果只是想离开窗口而不退出容器，需要使用“ctrl + p，ctrl + q”这组命令来离开容器，容器将会在后台保持运行。容器在后台运行的状态可以通过“docker ps”进行查看，例如：

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
7ab5341e698c        ubuntu:18.04        "/bin/bash"         About an hour ago   Up About an hour                        vigilant_kapitsa
```

通过上述命令可以看到，容器在后台运行，命令的ID为“7ab5341e698c”。如果希望再次进入到容器中，则可以通过attach命令再次进入到容器中。例如：

```
docker attach 7ab5341e698c
```

再次返回容器中，会继续看到容器内部shell的执行状态。如果返回容器中时，容器内部的shell正在执行命令，则会在shell处卡住。在shell处卡住时，通过“ctrl + c”命令能够结束当前命令的运行，也可以通过“ctrl + z”命令将执行的程序挂起，需要时通过“fg”恢复挂起程序的运行。

需要注意的是，在容器运行时，多个窗口通过attach命令连接容器，会进入到同一个shell中，导致shell的抢占，所以要尽量使用多个attach操作连接同一个container。

## 保存container

在docker运行过程中，安装好所需的软件工具后，可以通过“docker diff containner”命令看到有哪些修改，例如：

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
7ab5341e698c        ubuntu:18.04        "/bin/bash"         About an hour ago   Up About an hour                        vigilant_kapitsa

$ docker diff 7ab5341e698c
C /root
C /root/.viminfo
A /root/.vimrc
```

通过上述命令，可以看出在容器中，新增了viminfo和vimrc文件。为了保存这些修改，可以通过commit命令将container保存成一个新的image。命令如下：

```
docker commit -m "Add vimrc and viminfo" 7ab5341e698c myubuntu_1804:v0.1
```

通过上述命令，实现通过container 7ab5341e698c创建了一个名字为myubuntu_1804，tag为v0.1的image。下次运行docker的时候，可以直接运行该image。运行命令如下：

```
docker run -it myubuntu_1804:v0.1
```

通过该image运行的container中，包含了之前对viminfo和vimrc的更改，实现了对原容器的保存。

# MacOS

在MacOS上，默认使用的文件系统是不区分大小写的，这对于Linux编译来说会出现问题，所以需要创建一个区分大小写的扩展磁盘来存储buildroot项目文件。

在MacOS上，通过磁盘管理工具，可以在原有磁盘上新增一个添加到原磁盘上的卷宗。该卷宗可以与原磁盘共享存储空间，同时具有独立的磁盘格式。

新增卷宗时，将磁盘格式设置为“APFS区分大小写”，即可创建出一个新的区分大小写的卷宗。至此，MacOS上的磁盘准备工作就绪。

# 编译Buildroot

Buildroot是一个Linux平台上快速构建嵌入式Linux系统的框架，它可以使用menuconfig进行配置，实现快速构建Linux工具链、rootfs等环境的工具。

从Buildroot的官方网站上可以下载到Buildroot的源码包，网址在：https://buildroot.org/download.html。下载完成后进行解压缩，即可得到Buildroot的工作目录。

在该目录中，存在configs目录，其中包含了默认的config信息，可以通过默认配置快速实现构建。

下文中，将使用"qemu_mips64el_malta_defconfig"作为默认配置，来说明Buildroot的基本使用方法。

## Docker共享磁盘

为了能够在docker内部使用Buildroot，可以通过使用共享磁盘的形式将Buildroot挂载到docker内部，而不用将Buildroot放在容器的文件系统内部。这样能够很方便的保留Buildroot的编译结果，而不用通过保存container的形式去保存变更。

由于使用了共享磁盘作为Buildroot的存储环境，所以需要注意的是：

**该磁盘必须是区分大小写的，！！否则部分软件包编译会报错！！**

**该磁盘必须是区分大小写的，！！否则部分软件包编译会报错！！**

**该磁盘必须是区分大小写的，！！否则部分软件包编译会报错！！**

可以通过以下命令将共享目录挂载到container内部：

```
docker run -it -v ${PWD}:/dockershare myubuntu_1804:v0.1
```

上述命令中，${PWD}指的是当前目录（全路径），"/dockershare"指的是container内部可以看到的共享目录路径（全路径）。上述命令执行完成后，即可将当前目录挂载到docker container内部，也可以通过将${PWD}替换成其他全路径，实现指定路径的挂载。

需要注意的是，外部路径一定是存储了Buildroot的路径，并且该路径中可以存放区分大小写的文件。

## 配置

通过加载共享磁盘的方式进入容器后，可以进入"/dockershare/buildroot-2019.05”路径（本文下载的是2019.05版本的Buildroot），在该路径中，可以通过直接调用defconfig的形式进行快速配置，如：

```
make qemu_mips64el_malta_defconfig
```

配置完成后，需要调整部分选项信息，则可以通过"make menuconfig"进入菜单，进行修改。

这里可以将默认的软件包下载仓库调整为Buildroot的备份仓库，这样可以加快下载速度，避免部分软件包无法下载的情况。调整的配置路径如下：

```
 Symbol: BR2_PRIMARY_SITE [=http://sources.buildroot.net]                │  
  │ Type  : string                                                          │  
  │ Prompt: Primary download site                                           │  
  │   Location:                                                             │  
  │     -> Build options                                                    │  
  │       -> Mirrors and Download locations
  
将该值设置为“http://sources.buildroot.net”
```

修改完配置后，即可通过ecs进行后退，到最后一层退出时提示保存配置信息，保存即可。

## 编译

在配置完成后，即可进入编译步骤。编译命令如下：

```
make source # 提前将软件包全部下载，可省略
make        # 进行编译
```

上述编译步骤中，"make source"是可以省略的。但是通过“make source”可以将编译所需的全部软件包进行下载，后续进行编译即可，减少了编译过程中由于软件包无法下载导致的编译暂停。“make source”可以不执行，这样在编译的过程中，需要编译某个软件包时再下载，也是可以的。

Buildroot可以“make”命令完成编译，编译完成后，在output目录下存放着编译结果。至此，全部操作结束。


