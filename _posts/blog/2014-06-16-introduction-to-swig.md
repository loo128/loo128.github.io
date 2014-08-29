---
layout: post
title: 一个碉堡的工具SWIG
description: SWIG 是一个非常优秀的脚本绑定代码生成工具，可以将 C/C++ 代码与多种语言相集成，开源免费。
category: blog
---

一直知道有SWIG这个牛逼的存在，unity3d（genesis3d -.-）貌似也是用这个工具把底层的C++提供接口给C#使用。不久前的3.0.1版本又有了个重大更新，支持Javascript了，目前支持JavascriptCore，V8和node.js（木有SpiderMonkey）。一直很感兴趣，这下没理由不学习一下了。

##什么是SWIG

SWIG is a software development tool that simplifies the task of interfacing different languages to C and C++ programs. In a nutshell, SWIG is a compiler that takes C/C++ declarations and creates the wrappers needed to access those declarations from other languages including Perl, Python, Tcl, Ruby, Guile, and Java. SWIG normally requires no modifications to existing code and can often be used to build a usable interface in only a few minutes. 

##SWIG支持的c++语言特性

- Full C99 preprocessing.
- All ANSI C and C++ datatypes.
- Functions, variables, and constants.
- Classes.
- Single and multiple inheritance.
- Overloaded functions and methods.
- Overloaded operators.
- C++ templates (including member templates, specialization, and partial specialization).
- Namespaces.
- Variable length arguments.
- C++ smart pointers.

##SWIG目前支持的语言

- AllegroCL
- C# Mono
- C# MS .NET
- CFFI
- CHICKEN
- CLISP
- D
- Go language
- Guile
- Java
- Javascript Node.js
- Javascript V8
- Javascript WebKit(JavascriptCore)
- Lua
- MzScheme/Racket
- Ocaml
- Octave
- Perl
- PHP
- Python
- R
- Ruby
- Tcl/Tk

##references
- [SWIG官网](http://www.swig.org/)
- [SWIG仓库](https://github.com/swig/swig)
- [SWIG文档](http://www.swig.org/Doc3.0/index.html)

[Joshua]:    http://joshuastray.github.io  "Joshua"
