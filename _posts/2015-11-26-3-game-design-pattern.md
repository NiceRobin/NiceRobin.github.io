---
layout: post
title: Game Design Pattern笔记
categories: [技术]
tags: [game, design pattern]
fullview: false
comments: true
---

###1. Command
包裹操作指令，方便的实现undo和redo。

已经在纸牌游戏里面应用了。

在各种处理按键的程序中应用也很广泛

###2. flyweight
把共用的部分提取出来 而不是每一个元素都放一份
比如地形 不用把水的属性放到每一个实例里面，把属性放在一起 然后每个水的实例指向它

对于三消来说 view的renderinfo就可以公用 不用每个view都存一份

###3. 