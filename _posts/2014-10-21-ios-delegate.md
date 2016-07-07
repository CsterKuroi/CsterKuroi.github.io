---
layout: post
title: "delegate的多点回调？"
description: ""
category: 技术分享
tags: [iOS]
---
{% include JB/setup %}
# delegate不保留计数的多点回调？   
---

delegate的多点回调相对notification更加便捷，更多方便，让项目更好维护；并且是不保留计数了，当回调的对象已经不存在时会自动移出调用队列。
demo传送门：[点击我](https://github.com/zhangdadi/HDMultiPointCallNode)

### 使用方法：

重写delegate的set方法，在set方法里调用pushData，如下：

```
- (void)setDelegate:(id<HDMessageManageDelegate>)delegate {
    [_callNode pushData:delegate];
}
```
在需要回调的地方如下调用方式：

```
//图片下载完成，回调通知
            [_callNode callMultiPoint:^(id data) {
                [self callNewMessageDelegate:data obj:obj msgKing:msgKing];
            }];
```            

### 原理代码:
下面是多点回调类的代码：

HDMultiPointCallNode.h

```
/**
 *  不retain计数的多点回调
 */
@interface HDMultiPointCallNode : NSObject

/**
 *  加入委托对象
 *
 *  @param data delegate对象
 */
- (void)pushData:(id)data;

/**
 *  把delegate从回调队列里移除
 *
 *  @param index 索引
 */
- (void)popIndex:(NSInteger)index;

/**
 *  把delegate从回调队列里移除
 *
 *  @param data 对象实例
 */
- (void)popData:(id)data;

/**
 *  多点回调
 *
 *  @param block 需要回调的delegate
 */
- (void)callMultiPoint:(void (^)(id data))block;
```

HDMultiPointCallNode.m

```
@interface HDMultiPointCallNode ()
@property (nonatomic, weak) id data;
@property (nonatomic, strong) HDMultiPointCallNode *next;

@end

@implementation HDMultiPointCallNode

- (void)pushData:(id)data {
    [self popData:data];
    HDMultiPointCallNode *head = self;
    while (head.next != nil) {
        head = head.next;
    }
    
    HDMultiPointCallNode *newNode = [[HDMultiPointCallNode alloc] init];
    newNode.data                  = data;
    head.next                     = newNode;
}

- (void)popData:(id)data {
    HDMultiPointCallNode *head = self;
    HDMultiPointCallNode *temp = self.next;
    
    while (head.next != nil) {
        if (data == temp.data) {
            head.next = temp.next;
            temp.data = nil;
            temp      = nil;
        }
        head = head.next;
        temp = temp.next;
    }
}

- (void)popIndex:(NSInteger)index {
    HDMultiPointCallNode *head = self;
    HDMultiPointCallNode *temp = self.next;
    
    for (int i = 0; head.next != nil && i <= index; ++i, head = head.next, temp = temp.next) {
        if (i == index) {
            head.next = temp.next;
            temp.data = nil;
            temp      = nil;
        }
    }
}

- (void)callMultiPoint:(void (^)(id data))block {
    HDMultiPointCallNode *head = self;
    
    for (int i = 0; head.next != nil; ++i) {
        head = head.next;
        if (head.data != nil) {
            block(head.data);
        } else {
            [self popIndex:i];
        }
    }
}

@end

```
