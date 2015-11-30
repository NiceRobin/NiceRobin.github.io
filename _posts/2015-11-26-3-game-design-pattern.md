---
layout: post
title: Game Design Pattern笔记
categories: [技术]
tags: [game, design pattern]
fullview: false
comments: true

---



###1. Command

包裹操作指令，在能实现出一个漂亮的统一接口来处理按键输入。

最重要的是可以方便的实现Undo和Redo。

在纸牌游戏里面应用了。

###2. Flyweight

把共用的部分提取出来，而不是每一个元素都放一份。

比如实现多种地形中的水，不用把水的属性放到每一个实例里面，把属性放在一起，然后每个水的实例指向它。

比如对于三消来说，view的renderInfo就可以公用，不用每个view都存一份。

###3. Observer

用来解耦，一个常见的实现方法就是Events和EventsListener。

用链表来存储Observer是个好办法，可以方便的删除。比cocos2d使用的hash要聪明。

### 4. Prototype

一种用于创建对象的Pattern，基础的实现方式是clone，从一个已有的对象来快速创建出新的对象。比如cocos2d中的action。

同时还讨论了用prototype来实现OO的语言，比如js，prototype和class的不同之处在于，class的变量是属于instance的，而函数是属于类的，当创建一个新的instance的时候，变量并不会被复制，而prototype类的语言，变量同样是可以复用的，非常方便的特性。
<!--more-->
### 5. Singleton

保证只有一个实例（例如文件操作类），提供全局访问。

全局访问是个很容易被滥用的特性，同时它增加了耦合（因为必须include singleton的头文件），试访问控制变得很麻烦。

文章中提到了一些解决方案

1. 传递指针（这个有时候很麻烦，因为额外增加参数）

2. 可以使用父类，把原来singleton的指针放在父类里面。

3. 把很多singleton的指针作为一个singleton的成员，比如把game作为singleton，其他例如log，file，audio之类的都通过game来访问。

















