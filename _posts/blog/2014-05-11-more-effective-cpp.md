---
layout: post
title: 读书笔记：《More Effective C++》
description: 很久很久以前读过Effective C++，这第二卷现在才看。。。太懒了怎么办。。。
category: blog
---

1. pointer和reference：不会改变指向，或要重载类似operator[]这样的操作符时，使用reference，其他任何时候都是用pointer。
2. c++转型操作符：static\_cast基本与C风格转型相同，const\_cast只用于改变const和volatile，dynamic\_cast处理继承中的向下转型，reinterpret\_cast与编译器相关不具备移植性，通常用于函数指针的转换，实际上reinterpret\_cast可以随意转换4字节整数，包括int和指针。
3. 数组和多态不要混用。
4. 如非必要，不提供默认构造函数。
5. 对单参数constructor都声明为explicit。使用提供相同功能的函数，而不要使用隐式类型转换操作符（`operator 类型名() const;`），这也是为何string使用c_str,而没有隐式转换操作符。
6. 前置++返回引用，后置++返回const类型。对自定义类型，优先使用前置++，--。
7. 只有操作符重载能让程序更易读，易写，易理解才去做。永远不要重载&& || 和,
8. `new operator`调用`operator new`分配内存以及构造函数来初始化。`new operator`不能重载，`operator new`可以重载。placement new 是一个`operator new`的重载版本。同样的，我们一般调用的delete是`delete operator`，它调用析构函数和`operator delete`。所以，如果我们不需要构造或析构，可以显示使用`operator new`和`operator delete`，相当于malloc和free。[http://www.drdobbs.com/cpp/counting-objects-in-c/184403484](http://www.drdobbs.com/cpp/counting-objects-in-c/184403484 "counting objects in c++") 
9. 使用中异常：需要释放的资源无法被delete，如果在catch中delete就重复写了2次资源的清理（不好看），可使用smartpointer自动释放。
10. 构造异常:构造函数中发生异常使对象没有成功构造，c++不会默认调用他的析构函数进行清理，在catch语句中delete**完全不起作用**。所以要在构造函数中进行try-catch，清理并继续抛出异常。
11. 析构异常：避免异常从析构函数抛出。[http://bin-login.name/ftp/pub/docs/programming_languages/cpp/cffective_cpp/MAGAZINE/SU_FRAME.HTM#destruct](http://bin-login.name/ftp/pub/docs/programming_languages/cpp/cffective_cpp/MAGAZINE/SU_FRAME.HTM#destruct)
12. exception object 在被捕捉时总是发生复制，并且以静态类型复制。编译器会通过复制构造出一个临时对象，传递给catch，所以如果catch的参数是以by value传递，会发生两次复制！！！catch中的参数只允许两类转换，指针到void*的转换，和子类到父类的转换。catch采用fit first策略，所以exception 子类的catch一定要写在父类前。
13. 捕获异常时，通过指针传递，需要delete。通过值传递有2次复制，且如果catch参数是exception object的父类，那么子类的成员会被切割掉。所以最佳方式是在catch中by reference 传递。
14. 不要为模板指定exception specification，因为不可能不知道其参数类型可能抛出什么异常。a函数调用b函数，如果b没有exception specification 那么a也不要有。set_unexpected设置自己的处理函数，可以在其中抛出自定义的异常。
15. 异常处理机制会让程序体积变大，速度变慢。如果可以确保没有使用任何异常处理，链接的第三方库也没有，可以关闭编译器的异常处理支持。尽量少使用异常处理，只在必须的地方使用try和exception specification。
16. 80-20原则。
17. 


[Joshua]:    http://joshuastray.github.io  "Joshua"
