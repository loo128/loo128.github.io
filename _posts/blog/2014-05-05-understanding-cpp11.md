---
layout: post
title: 读书笔记：《深入理解C++11》
description: 第一篇，要开始好好写。。。
category: blog
---


##第4章
- ++i返回左值，i++返回右值。

##第5章

enum：

- enum是非强作用域类型，具名的的enum类型的名字和成员的名字是全局可见的，可能会造成污染。
- enum进行数值比较时总是会默认转为int，所以也可以与其他enum比较，编译器警告但不报错。class中的数据不会被默认转为int。
- 大多数系统中，函数参数是int可以通过寄存器传递，struct/class只能放在栈上，所以enum有此性能优势。
- 符号不确定，不同编译器不同。

enum class/struct：

- 优势：强作用域，不会默认转为int，可以指定除wchar_t外的类型。
- 是POD类型。
- 可以指定更小的基本类型，节省内存。
- 可以指定类型符号，消除编译器差别。

智能指针：

- 可以对unique_ptr使用move
- shared_ptr共享一个堆分配对象的内存，reset只是引用计数-1.

基于跟踪的gc：

- mark-sweep (spidermonkey使用这种方式)
- mark-compact
- mark-copy

c++11的最小垃圾回收：你™在逗我！
##第6章

constexpr编译期常量，如果没有在代码中显示地使用，不会产生实际数据。
constexpr用于自定义类型，需要有constexpr修饰的构造函数，且函数体必须为空，初始化列表只能由常量赋值。

变长模板：偏特化+递归构造来使用。。。

原子类型，默认加锁。原子操作可以指定memory\_order.

thread_local线程生命周期。

quick\_exit相比exit不执行对象的析构函数。at\_quick\_exit可以注册至少32个函数，调用顺序与注册顺序相反。

##第7章

nullptr是编译器关键字，编译期常量，是nullptr\_t类型的一个值。nullptr\_t定义在cstddef：

    typedef decltype(nullptr) nullptr_t//蛋生鸡。。。

nullptr\_t类型只可以转换成指针类型，if(nullptr)或if(nullptr==0)都无法通过编译。 

=default和=delete显示控制默认缺省函数，=delete可以禁止函数参数的转换，不应和explicit混用，带来语义上的混乱。

lambda编译器一般通过仿函数(functor、function object)实现，所以实际是仿函数的语法糖。

传值捕捉列表，传递的值在lambda定义就确定了，不随父作用域中的值改变。lambda默认是const的，值传递的变量不可改变。

##第8章

    alignas(alignof(double)) char c;
alignas参数必须是2的n次方。std::align动态调整对齐方式。。。略imba。。性能如何？

增加[[]]属性为了编译器可以做一些代码优化。
[[noreturn]]函数不会返回：抛出异常，终止程序，无限循环等。
[[carries_dependency]]暂无编译器支持。。只适用于弱内存模型平台，作用有限。

raw string literal使用R"()"：
  
    cout<<R"(hello,\n
         world)"<<endl;
    hello,\n
            world

##C++11弃用的特性

1. auto，register不能再用于声明变量的存储方式
2. export保留但无意义
3. auto_ptr
4. bind1st，bind2nd
5. adapter