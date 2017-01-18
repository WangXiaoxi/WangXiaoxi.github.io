---
title: iOS与Android中，给View设置优先级
date: 2017-01-19 00:06:02
tags: [iOS, Android]
---

## 背景
在开发中，常常会有这样的需求 `[-10-Label-5-Icon-10-]`，水平放置一个 Label 与一个 Icon（或 Label ），其中第一个长度不固定，后面的 Icon 紧随 Label 动态调整，但是不能超出屏幕范围，同时要保证位于右边的 Icon（或 Label ）不被压缩。

## 问题
iOS 上只需要设置约束的优先级与压缩阻力的属性，视图在绘制的时候会做好这一切的。
Android 的小伙伴在此遇到了麻烦，最后妥协于 HardCode。
个人感觉 Android 的布局机制是要更优于 iOS 的（其实我是卧底😅），更不愿看 HardCode 解决此类问题。下班回家后操起已尘封的 AS，几番尝试后，答案还是很显而易见的。

## Android XML文件配置

``` xml
<android.support.v7.widget.LinearLayoutCompat
        android:layout_width="wrap_content" // 此处注意使用 wrap_content
        android:layout_height="20dp"
        android:orientation="horizontal">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="20dp"
            android:text="hahahahahhahahaaaaaahahhaaaaaaaaaaaaaaaaa"
            android:ellipsize="end"
            android:layout_weight="1" // 设置权重
            />

        <Button
            android:layout_width="20dp"
            android:layout_height="20dp"
            android:background="@color/colorPrimaryDark"
            android:text="OK"
            android:id="@+id/button" />

</android.support.v7.widget.LinearLayoutCompat>
```

## iOS属性设置

```objectivec
[label setContentHuggingPriority:UILayoutPriorityDefaultLow forAxis:UILayoutConstraintAxisHorizontal];
```

