---
layout: post
title: JSB中开启SpiderMonkey的BaseLine
description: 
category: blog
---

cocos英文论坛上一个网友提到开启SpiderMonkey的Baseline，他的游戏从30帧涨到60帧。今天试了一下，果然快很多。在ScriptingCore的createGlobalContext函数里添加：

    JS::ContextOptionsRef(_cx).setBaseline(true);

用了一个排序的算法循环执行10000次，速度快了10倍多，与使用chrome的v8测试结果基本一样了。简直碉堡了，jsb的性能又能提上去很多，已经合并到cocos2d-js的主仓库了。

查了下资料，这个Baseline是SpiderMonkey中一个新的JIT Compiler，比默认使用的JaegerMonkey和IonMonkey更快，占用内存更少。

Reference：

1. [https://blog.mozilla.org/javascript/2013/04/05/the-baseline-compiler-has-landed/](https://blog.mozilla.org/javascript/2013/04/05/the-baseline-compiler-has-landed/)
2. [http://www.tuicool.com/articles/qu2i2a](http://www.tuicool.com/articles/qu2i2a)


[Joshua]:    http://joshuastray.github.io  "Joshua"
