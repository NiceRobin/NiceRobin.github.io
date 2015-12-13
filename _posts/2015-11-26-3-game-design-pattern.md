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

3. 把很多singleton的指针作为一个singleton的成员，比如把game作为singleton，其他例如log，file，audio之类的都通过game来访问。我喜欢这种。

### 6. State

也就是状态机啦，比较有意思的是基于栈的状态机，可以把老的状态压入栈，然后再压人新的状态，这样当新的状态结束，可以方便的回到原来的状态。

当然这种使用栈的方式也不是很令人惊奇，因为这更像一种理所当然的实现方法。做前进后退本来也是要用栈的。

我一直不是很喜欢状态机，因为状态变多之后，转移函数和条件就会变得很不清晰，比如三消链状处理函数，实际上是也可以通过状态机来写的，因为本质上就是从一个阶段转化到另一个阶段，但是三消这种情况，我觉得状态机不是一种很灵活的处理方式。把复杂的逻辑粗暴的分成了状态。写起来感觉不是很舒服。

另一个非常赞的主意是状态开始时候的onEnter函数，可以把关于本状态的代码都放到一起，比起把一些代码放到状态转移函数里面或者上一个状态里面要好很多。

### 7. Double Buffer

简单的说就是要按顺序读取一些值，但是前面的值在读取过程中有可能改变后面还没被读取的值，所以double buffer就是读取的时候读旧值，改的时候改新值。全部处理结束之后，把新值和旧值交换。

### 8. Game Loop & Update

就是常见的loop和update，各种游戏引擎都实现了得那种。

很赞的是固定时间update的实现方法。

    double previous = getCurrentTime();
    double lag = 0.0;
    while (true)
    {
      double current = getCurrentTime();
      double elapsed = current - previous;
      previous = current;
      lag += elapsed;
    
      processInput();
    
      while (lag >= MS_PER_UPDATE)
      {
        update();
        lag -= MS_PER_UPDATE;
      }
    
      render();
    }

### 9. Bytecode
简要的介绍了基于栈的脚本语言的实现方式。

用栈处理参数的方式：

    0 func
    1 pram1(push to stack)
    2 param2(push to stack)
    3 run(pop param from stack)

### 10. Subclass Sandbox & Type Object

在基类里面提供一些操作，然后子类里面去调用。非常好的办法，比我在island里面搞的那个不成功的sandbox要好很多。

type object 就是我在island里面用来定义元素种类的方法，使用描述元素的type和一个通用的生成元素的方法，而不是定义很多子类。

比起使用表，还是json的表现力更强，麻烦的是需要自己写工具来表现每种元素的继承关系。

### 11. Component

本质上来说就是一种代码的拆分，不管是把每个sprite的功能拆分成component，还是把游戏的逻辑拆分成logic。

component之间的通讯，最解耦的办法就是message。还可以通过他们的容器，这种快速而且比较直观。

### 12. Event Queue

主要是用于那些不必同步执行，同时花费很多时间的操作，比如读写文件，网络请求，可以把他们放到队列里面，好处是主要行为不至于暂停，同时统一组织还有方便优化的好处，因为增加操作的时候和已经在队列里面的操作进行合并。

同时介绍了一个很赞的循环队列的实现。

另外一方面的event也可理解成缓存事件，经典的例子就是键盘操作，因为程序一次只能处理一个操作，那么肯定要用队列把曹植存储起来。

### 13. Service Locator

例子是给单例增加了一层抽象，这样方便以后进行替换，实际上就是统一接口，方便更换实现，

这个还是很重型的pattern，要写很多纯结构的代码。

### 14. Data Locality

优化技巧，对cpu的缓存优化，总体来说块状的排列数据肯定是缓存友好的。

里面有个很厉害的例子。

一般方案：

    for sprite in spriteArr
        spirte.renderComponent().update()
        spirte.aiComponent().update()

对缓存更友好的方案：

    for rc in renderComponentArr
        rc.update()
    for ac in aiComponentArr
        ac.update()
        
核心就是减少指针，使用静态数组。

同时还要注意数组内的不活跃元素，它们被加载到缓存，但是不会参与运算。

另外还提到那些不参与运算的值可以放到类外面，使用指针，这样也可以提高cache match的几率。

### 14. Dirty Flag

很常用，广泛意义上来说就是延迟更新，在需要用的时候才依据是否设置为dirty来更新，否则就一直不更新。

渲染的例子中，延迟更新还带来了减少计算量的好处，apx2d的dirty是减少自身矩阵的计算，这里更进一步cache了整个sprite的变换矩阵。

### 15. Object Pool

避免创建和内存碎片，这里面有一些优化还是做的很极致的，比如尽量使用固定长度的数组，通过union来维护未激活的例子等方法。

值得关注的一点是pool对新对象的初始化，还有垃圾回收时候因为pool内元素导致的问题。

### 16. Spatial Partition

空间划分，这部分我还是没有实际操作过，四叉树八叉树之类的东西只是听说过，以后有接触之后应该会有比较深得理解吧。



