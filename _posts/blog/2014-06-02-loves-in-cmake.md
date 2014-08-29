---
layout: post
title: 爱上CMake
description: 
category: blog
---

前几天看了下-js比-x少了linux和wp8工程，wp8的jsb编译工作微软正在做，linux感觉没理由不做，而且-x已经支持了所以应该没什么难度，放假花了一天时间搞定了，总结一下过程。

1. 编译SpiderMonkey v28的linux静态库，包括32位和64位。这个没什么难度，按照mozilla官网的说明就可以了，比windows上方便多，不用从mozbuild，nspr开始编译。
2. 编写所有绑定模块的CMakelists.txt，按模块生成静态库。
3. 编写js-test和js-moonwarriors的CMakelist.txt，生成可执行文件。
4. 所有工程添加proj.linux，只需要一个简单的main.cpp：
    
```
int main(int argc, char **argv)
{
    // create the application instance
    AppDelegate app;
    return Application::getInstance()->run();
}
```
TODO: cocos console支持linux工程编译。

写了几个CMake文件后，发现这东西太好了。。。大概意思就是一套通用的编译配置，会按照不同平台生成相应的vcxproject，makefile等。写法十分灵活，比写android的mk好多了。。。总结一下常用的命令：

```
#set定义一个变量，后面使用${PLATFORM_FOLDER}就会替换为linux
set(PLATFORM_FOLDER linux)

#包含路径
include_directories(
  project/Classes
  ../../frameworks/js-bindings/bindings/auto
)

#链接库路径
link_directories(
${CMAKE_CURRENT_SOURCE_DIR}/frameworks/js-bindings/cocos2d-x/external/jpeg/prebuilt/${PLATFORM_FOLDER}
）

#生成可执行文件
add_executable(${APP_NAME}
  ${SAMPLE_SRC}
)

#生成静态库
add_library(jsbinding STATIC
  ${JSBINDING_SRC}
)

#链接静态库，这个顺序不能乱写，如果a依赖b，a必须写在b前面，否则一堆unresolved symbol这类错误
target_link_libraries(${APP_NAME}
  jsb_spine
  spine
  jsb_studio
  cocostudio
  jsb_builder
  cocosbuilder
  jsb_chipmunk
  chipmunk_static
  jsb_extension
  extensions
  audio
  jsb_localstorage
  jsb_network
  jsb_ui
  jsbinding
  cocos2d
  js_static
)

#在build前可以执行一些命令，常用的remove，remove_directory，copy，copy_directory等
pre_build(${APP_NAME}
  COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/main.js ${APP_BIN_DIR}/main.js
)

#用来指定生成的二进制文件输出路径，最好在一个新建文件夹执行cmake，make，保持源码文件夹的干净
set_target_properties(jsbinding
    PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
)
```

可以通过这种方式判断系统是32位还是64位：

```
# architecture
if ( CMAKE_SIZEOF_VOID_P EQUAL 8 )
set(ARCH_DIR "64-bit")
else()
set(ARCH_DIR "32-bit")
endif()
```
另外CMake有一些内置的变量，可以帮助做一些编译的控制：[http://blog.sina.com.cn/s/blog_5413483701016dhf.html](http://blog.sina.com.cn/s/blog_5413483701016dhf.html)

官方文档：[http://www.cmake.org/cmake/help/cmake2.6docs.html](http://www.cmake.org/cmake/help/cmake2.6docs.html)


[Joshua]:    http://joshuastray.github.io  "Joshua"
