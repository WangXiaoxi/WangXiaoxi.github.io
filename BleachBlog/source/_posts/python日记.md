---
title: python日记
date: 2016-01-25 00:54:42
tags: python
---

周末闲来无事，简单学习了一下Python，在做循环的时候，不论怎么调试修改，始终在编译的时候报错，也是比较郁闷。排查了制表符与空格的嫌疑之后，发现是自增运算符出现了问题，google之后才发现原来Python取消了`++`的运算方式,感觉比较好玩。

__正如所言：__*`只用一种方式解决问题`*

看到这段儿代码时，深深地被吸引到了

    def triangles():
	    b = [1]
	    while True:
	        yield b
	        b = [1] + [b[i] + b[i+1] for i in range(len(b)-1)] + [1]
	
