---
layout: post
title: "ios内存分配方式"
description: ""
category: 技术分享
tags: [iOS]
---
{% include JB/setup %}
# ios内存分配方式
---
![1](http://zhangdadi.github.io/image/ios/memory/1.jpg)

你看到上面这图，有什么想法没？我的理解:stactStr1，stactStr2和stactStr3本身是在栈中，分别指向常量区的"123"和"12"的内存地址，所以stactStr1和stactStr2的指向的内存地址一样，因为都是"123"；
而alloc init是对堆的操作，NSString *heapStr1 = [[NSString alloc] initWithFormat:@"123"]；从堆中申请空间，返回的是这空间的首地址，这空间里的数据是"123"这字符，所以heapStr1和heapStr2的内存地址不同，虽然它们都是"123"。

---

还有,我觉得[NSString alloc] initWithFormat:@"123"]和[NSString stringWithFormat:@"123"];申请的内存过程都是一样的,都一样是在堆中,不过一个是要你自己手动释放,一个是api内部已经已经设置成的autorelease,而不管是[str1 copy]还是[NSString stringWithString:str1]其实都是把str1指向的内存地址反回去而已,如下图：

![2](http://zhangdadi.github.io/image/ios/memory/2.jpg)

---

还有我发现网上很多人说什么文字常量区和全局静态区,说:文字常量区是保存常量的,我一直不明白这文字常量区是什么,怎么来?我发现根本没有什么文字常量区,常量和全局变量都是一样保存在全局静态区里,如有不对望大神指出,下面是验证示图:

![3](http://zhangdadi.github.io/image/ios/memory/3.jpg)