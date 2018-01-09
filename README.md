# A-TRY-ON-AHK
之前用Python写过一个简单的小脚本，Python是好用，但不能给没装过环境小伙伴共享。	

于是我找到了AutoHotKey这款脚本语言，并粗略的学习了一下。

这是一款基于AutoIt开源代码开发的脚本语言，添加了更多实用的特性<del>，是居家旅行必备的好帮手</del>。	

>特别感谢 Jonathan Bennett，他于 1999 年把 AutoIt v2 作为自由软件慷慨地发布出来，
使其成为我以及世界上其他许多人节省时间的工具。
此外，AutoHotkey 中许多针对 AutoIt v2 命令集的增强功能以及 Window Spy 和旧的脚本编译器都是直接改写自 AutoIt v3 源代码。
所以为此同样感谢 Jon 和 AutoIt 的其他开发人员。<br>
>最后，AutoHotkey 离开了这些人也不会有今天。<br>
>~ Chris Mallett
---


# 快速入门

## 0x00 创建脚本

每个脚本都是需由程序 (AutoHotkey.exe) 执行的包含命令的纯文本。

脚本中还可以包含 **热键** 和 **热字串** 或者甚至完全由它们组成。

不过, 在不包含热键和热字串时, 脚本会在启动后从上往下按顺序执行其中的命令。

安装了AutoHotKey环境可以直接运行脚本文件*.ahk，也可以编译成exe文件在各种Windows平台下直接运行。

## 0x01 第一段代码

可以使用 Run 命令来其中程序, 文档, URL 或快捷方式。例如：

	Run Notepad

	Run C:\My Documents\Address List.doc

	Run www.baidu.com

## 0x02 程序执行方式

顺序执行脚本中的代码,

或者使用热键和热子串：

热键:

	**hotkey**::
	
		...
		
		(*code here*)
		
		...
		
	return
	
## 0x03 调试

调试脚本： 

	ListVars
	Pause

当脚本执行到这两行时, 会显示所有变量当前包含的内容供您检查. 

当您准备恢复时, 可以通过 File 或托盘菜单取消暂停. 然后脚本会继续执行，

直到遇到下一个“断点”（如果有）。