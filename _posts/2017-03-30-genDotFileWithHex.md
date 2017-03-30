---
layout: post
category: "linux"
description: "通过反汇编文件生成函数调用关系图"
title:  "通过反汇编文件生成函数调用关系图"
date: 2017-03-30 15:14:35+00:00
tags: [Default]
---

今天尝试编写了一个通过反汇编文件生成 Mips 函数调用关系图的脚本。

脚本原理：

* 判断函数名称，并记录
* 判断函数内对其它函数的调用，并记录被调用函数的名称
* 如果 “函数 -> 被调用函数” 关系没有被记录，则存储到列表中
* 遍历列表，打印调用关系

脚本代码如下：
```
#! /usr/bin/python

# Assemble file
file = open("a.hex");
lines = file.readlines()

def isFuncName(line=""):
    if line.__contains__(">:"):
		return True
	else:
		return False

def isJalName(line=""):
    if line.__contains__("jal"):
		return True
	else:
		return False

def getFuncName(line=""):
    left = line.find("<")
	right = line.find(">") + 1

	if right <= left:
		return ""
	else:
		return line[left:right]

def genDotFile(lst=list()):
    print "digraph graphic {"
	for l in lst:
		print "    " + l.keys()[0] + " -> " + l.values()[0] + ";"
	print "}"

funcName = ""
targetName = ""
lst = list()

for line in lines:
	if isFuncName(line):
		funcName = getFuncName(line)
	elif isJalName(line):
	    targetName = getFuncName(line)

		if targetName != "":
			if {funcName: targetName} not in lst:
				lst.append({funcName: targetName})

genDotFile(lst)

file.close()
```

运行脚本，将输出指向到 dot 文件中，然后使用 dot 命令对其进行编译，命令如下：

```
dot -Tsvg test.dot -o test.svg
```

最终的输出文件 test.svg 就是函数调用关系图。