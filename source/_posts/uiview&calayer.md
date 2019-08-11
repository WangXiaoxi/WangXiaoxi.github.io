---
title: UIView 与 CALayer
tags: [iOS]
---

## UIView VS CALayer

### UIView

在 iOS 程序开发中，`UIView` 作为视图显示的基础组件，是用户交互的最主要的组成部分。主要包含以下职能：

1. 内容绘制与动画
   1. 通过 UIKit 或 Core Graphics 绘制内容
2. 布局与子视图管理
   1. 一个 View 可能包含 0 个或多个子 View
   2. 调整子视图的大小与位置
   3. 通过 AutoLayout 来约束视图之间的布局关系
3. 事件相应
   1. 作为 `UIResponder` 的子类，可以相应触摸或其它事件
   2. 通过 `Gesture Recognizers` 实现常用的手势识别

### CALayer

CALayer 常作为 UIView 的属性，实现内容绘制，不具备交互能力。CALayer 也包含自身的属性，如 background color、border、shadow。

可以通过 position，size，transform 来实现一些动画。还可以通过实现 [CAMediaTiming](https://developer.apple.com/documentation/quartzcore/camediatiming) 协议完成稍复杂的动画。 

通过 UIView 创建的 layer，view 会将自动将自己设置为 layer 的代理。

### Bounds

表示大小和位置，相对于自身的坐标系统。

### Frame

表示大小和位置，相对于父视图的坐标系统。

