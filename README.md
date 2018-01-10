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

**顺序执行脚本中的代码**

或者使用热键和热子串：

热键:

	**hotkey**::
	
		(*code here*)

	return


## 0x03 调试

通过 DBGp 可以支持调试功能，DGBp 是一种常见的支持多语言和调试器 UI 通信的调试器协议。

>SciTE4AutoHotkey 是一个免费的基于 SciTE 的 AutoHotkey 脚本编辑器. 除了 DBGp 支持, 它还为 AutoHotkey 提供了语法高亮, 调用提示, 参数信息和自动完成, 以及其他拥有的编辑特性和辅助工具.

>>http://www.autohotkey.net/~fincs/SciTE4AutoHotkey_3/web/

>Notepad++ DBGp 插件,一个可作为 Notepad++ 插件使用的 DBGp 客户端. 它设计用于 PHP，不过用于 AutoHotkey 时同样工作地很好。


代码调试： 

	ListVars
	Pause

当脚本执行到这两行时, 会显示所有变量当前包含的内容供您检查. 

当您准备恢复时, 可以通过 File 或托盘菜单取消暂停. 然后脚本会继续执行，

直到遇到下一个“断点”（如果有）。


## 0x04 变量

变量的类型: AutoHotkey 中没有明确的变量类型. 然而, 只包含数字 (可以含有小数点) 的变量进行数学运算或比较时, 会被自动转换为数值. (为了提高性能, 在内部会对数字进行缓存以避免与字符串之间的转换.)

变量的作用域和声明: 除了函数中的 局部变量, 其他所有变量都是全局的; 即可以在脚本的任意位置读取或修改它们的内容. 除了在函数页面注明的情况，变量都是不需要声明的；使用它们的时候它们就产生了（每个变量初始为空）。

变量的名称: **变量名不区分大小写 (例如, CurrentDate 等同于 currentdate).** 变量名可以含有多达 253 个字符, 并且可以由字母, 数字以及后面的标点组成: # _ @ $


给变量赋值:

	MyNumber = 123
	MyString = This is a literal string.
	CopyOfVar = %Var%   **(和 = 运算符一起使用时, 需要使用百分号来获取变量的内容.)**
	*另一种写法:(  CopyOfVar := Var  )*

获取变量的内容: 

	MsgBox The value in the variable named Var is %Var%.
	CopyOfVar = %Var%

	
## 0x05 表达式

表达式中的变量名称不用包围在百分号中（伪数组和其他的双重引用除外）。所以, 为了与变量区别, 原义的字符串必须用双引号包围. 例如：

	if (CurrentSetting > 100 or FoundColor <> "Blue")
		MsgBox The setting is too high or the wrong color is present.
	
保存表达式的结果: 要把结果赋值给变量, 请使用 := 运算符. 例如：

	NetPrice := Price * (1 - Discount/100)
	
	
布尔值: 要计算表达式结果为真还是假时 (例如 IF 语句), 表达式结果为空或0被视为假, 而其他所有结果都视为真	
	
单词 true 和 false 是值分别为 1 和 0 的内置变量. 使用它们可以增加脚本的可读性
	
	
接受数值输入的命令, 函数和表达式通常可以支持 15 位的浮点数精度. 对于整数, 可以支持 64 位有符号整数, 其范围从 -9223372036854775808 (-0x8000000000000000) 到 9223372036854775807 (0x7FFFFFFFFFFFFFFF). 此范围外的任何整数不受支持, 并可能产生错误的结果. 与之相比, 整数的算数运算结果超出此范围时会产生溢出 (例如 0x7FFFFFFFFFFFFFFF + 1 = -0x8000000000000000).	
	

## 0x06 函数	

	Add(x, y){
		return x + y
	}
	Var := Add(2, 3)
	
ByRef 参数: 从函数的角度看, 参数本质上是 局部变量, 除非它们被定义为 ByRef引用, 例如:
	Swap(ByRef Left, ByRef Right)
	{
		temp := Left
		Left := Right
		Right := temp
	}

可选参数:
	Add(X, Y, Z:=0) {
		return X + Y + Z
	}
	
内置函数:

在内置函数参数列表末尾的任何可选参数可以完全省略. 例如, WinExist("Untitled - Notepad") 是有效的, 因为它的其他三个参数被认为是空的.

如果脚本定义了与内置函数同名的函数, 那么内置函数会被覆盖. 例如, 脚本会调用它自己定义的 WinExist() 函数来代替标准的那个. 然而, 这样脚本将无法调用原来的函数.

在 DLL 文件中的外部函数可以使用 DllCall() 调用.


## 0x07 流程控制

if-else:

	if (x < y) {
		...
	}
	
	if WinExist("Untitled - Notepad") {
		WinActivate
	}
	
	if IsDone {
		...
	} else {
		...
	}
	
for循环:

**For Key [, Value] in Expression**

	;列出对象中的键值对：
	colours := Object("red", 0xFF0000, "blue", 0x0000FF, "green", 0x00FF00)
	
	;上面的表达式可以直接代替下面的“colours”：
	for k, v in colours
		s .= k "=" v "`n"
	MsgBox % s

while循环:

	while (*Expression*){
		...
	}
	
continue & break:

和C语言中一样	

Pause暂停:

	#p::Pause ; 按一次 Win+P 会暂停脚本. 再按一次则取消暂停.

	
## 0x08



