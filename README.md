# A-TRY-ON-AHK
之前用Python写过一个简单的小脚本，Python是好用，但不能给没装过环境小伙伴共享。	

于是这两天空闲时间我找到了这款脚本语言：AutoHotKey。	

这是一款基于AutoIt开源代码开发的脚本语言，添加了更多实用的特性<del>，是居家旅行必备的好帮手</del>。	

---


# 快速入门

## 0x00 创建脚本

每个脚本都是需由程序 (AutoHotkey.exe) 执行的包含命令的纯文本。

脚本中还可以包含 **热键** 和 **热字串** 或者甚至完全由它们组成。

不过, 在不包含热键和热字串时, 脚本会在启动后从上往下按顺序执行其中的命令。

安装了AutoHotKey环境可以直接运行脚本文件*.ahk，也可以编译成exe文件在各种Windows平台下直接运行。

## 0x01 Run命令

可以使用 Run 命令来其中程序, 文档, URL 或快捷方式。例如：

>Run Notepad
Run C:\My Documents\Address List.doc
Run C:\My Documents\My Shortcut.lnk
Run www.yahoo.com
Run mailto:someone@somedomain.com