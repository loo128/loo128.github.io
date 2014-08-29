---
layout: post
title: 在sublime text配置Python环境
description:
category: blog
---

试了Python自带的IDLE，不好用。。其他ide又太重量，还是sublime好哈哈。
1.Tools -> Build System -> New Build System 新建一个Python3.sublime-build文件。

```
{
    "cmd": ["python", "-u", "$file"],
    "path":"D:/SDK/Python34",
    "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
    "selector": "source.python"
}
```
保存，Tools -> Build System 选择Python3，Ctrl+空格就可以运行py了。

2.安装SublimeCodeIntel增加代码提示

`Ctrl+Shift+P`选择Install Package等一会输入SublimeCodeIntel安装就可以了。貌似可以自行配置reference路径带进行代码提示，暂时用不到，不折腾了。。


[Joshua]:    http://joshuastray.github.io  "Joshua"
