---
layout: post
title: "UIScrollView属性总结"
description: ""
category: 技术分享
tags: [iOS,UIScrollView]
---
{% include JB/setup %}
# UIScrollView属性总结
---

属性类型 | 属性名称 | 属性作用
:------------ | :------------- | :------------
CGPoint | contentOffSet  | 监控目前滚动的位置
CGSize | contentSize  | 滚动范围的尺寸大小
UIEdgeInsets | contentInset  | 视图在scrollView中的位置
BOOL | directionalLockEnabled  | 控件是否只能在一个方向上滚动
BOOL | bounces  | 控制控件遇到边框是否反弹
BOOL | alwaysBounceVertical  | 控制垂直方向遇到边框是否反弹
BOOL | alwaysBounceHorizontal  | 控制水平方向遇到边框是否反弹
BOOL | pagingEnabled  | 控制控件是否能够整页滚动
BOOL | scrollEnabled  | 控制控件是否能够滚动
BOOL | showsHorizontalScrollIndicator  | 是否显示水平滚动条
BOOL | showsVerticalScrollIndicatorInsets  | 是否显示垂直滚动条
UIEdgeInsets | scrollIndicatorInsets  | 指定滚动条在scrollView中的位置
UIScrollViewIndicatorStyle | indicatorStyle  | 指定滚动条的样式，有默认，黑色，白色
float | decelerationRate  | 改变scrollView的减速点的位置
BOOL | tracking  | 监控当前目标是否正在被跟踪
BOOL | dragging  | 监控当前目标是否正在被拖拽
BOOL | decelerating  | 监控目标是否正在减速
BOOL | contentOffSet  | 监控目前滚动的位置
CGPoint | delaysContentTouches  | 控制视图是否延时调用开始滚动的方法
BOOL | canCancelContentTouches  | 控制控件是否接触取消touch事件
float | minimumZoomScale  | 缩小的最小比例
float | maximumZoomScale  | 放大的最大比例
float | zoomScale  | 设置变化的比例
BOOL | bouncesZoom  | 控制缩放的时候是否会反弹
BOOL | zooming  | 判断控件的大小是否正在改变
BOOL | zoomBouncing  | 判断是否正在进行缩放反弹
BOOL | scrollsToTop  | 控制控件滚动到顶部
