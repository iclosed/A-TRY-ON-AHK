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

	
## 0x08 鼠标控制

强制无条件安装鼠标钩子:

	#InstallMouseHook

AutoHotkey 不会无条件安装键盘和鼠标钩子, 因为它们合起来至少占用 500 KB 的内存 (但如果已经安装键盘钩子, 此时再安装鼠标钩子只需要增加约 50 KB 的内存, 且反之亦然). 因此, 一般只有在脚本包含一个或多个鼠标 热键 时才会安装鼠标钩子. 还会为 热字串 进行安装, 不过可以通过 #Hotstring NoMouse 禁用.

此指令还会让脚本变成 持续运行的, 这意味着应该使用 ExitApp 结束脚本.


### Click:

在指定坐标处点击鼠标按钮。它还可以按下鼠标按钮，转动鼠标滚轮或移动鼠标。

这里有一些常见用法的例子:

	Click 在鼠标光标的当前位置点击一次鼠标左键. 
	Click 44, 55 在 44, 55 坐标 (基于 CoordMode) 处点击一次鼠标左键. 
	Click right 44, 55 与上述相同, 不过这里点击鼠标右键. 
	Click 2 在光标的当前位置点击两次鼠标左键 (即双击). 
	Click down 按下鼠标左键不放. 
	Click up right 释放鼠标右键. 
	Click %x% %y% 由于 click 不支持 表达式, 所以变量应该括在百分号中. 

Click 后可以跟零个或多个下列项. 每个项之间至少需要一个空格, tab 和/或逗号分隔. 除了ClickCount必须放在坐标后面（如果使用了坐标），各项可以按任何顺序出现。

X, Y: 在点击前, 鼠标光标要移动到的 x/y 坐标. 如果省略, 那么使用光标的当前位置.
**(坐标相对于活动窗口, 除非曾使用 CoordMode 改变了这个设置)**
>这个很重要，我刚开始用的时候坐标总是搞错，具体的在后面会说。

按钮名称：Left（默认）、Right、Middle（或仅使用这些名称的首个字母），或鼠标的第四或第五个按钮（X1 或 X2）。注意: 与 MouseClick 不同, 这里左键和右键的行为在所有系统上都是一致的, 即使用户通过系统控制面板交换了按钮的功能.

鼠标滚轮：指定 WheelUp 或 WU 来向上转动滚轮（远离您的方向），指定 WheelDown 或 WD 来向下转动滚轮（靠近您的方向）。在 v1.0.48+, 还可以指定 WheelLeft (或 WL) 或 WheelRight (或 WR) (不过它们在 Windows Vista 以前的系统上无效)。对于 ClickCount (下面的), 指定滚轮要转动的格数。然而, 有些程序不接受鼠标滚轮转动的格数 ClickCount 大于 1 的情况，这种情况可以使用循环来解决。

ClickCount：鼠标要点击的次数（例如：Click 2，Click 100, 200, 2）。如果省略, 那么点击鼠标一次. 如果指定了坐标, 那么 ClickCount 必须放在坐标后面. 指定零（0）来移动鼠标而不进行点击（例如：Click 200, 0, 100）。

Down 或 Up: 这两个单词通常省略, 此时每次点击包括按下事件和接着的弹起事件. 否则, 指定 Down (或字母 D) 来按下鼠标按钮不放. 之后, 使用单词 Up (或字母 U) 来释放鼠标按钮.

Relative: 使用单词 Rel 或 Relative 会把指定的 X 和 Y 坐标视为距离当前鼠标位置的偏移. 换句话说, 会把光标从当前位置往右移动 X 像素 (负值则往左) 且往下移动 Y 像素 (负值则往上).

Click 使用的发送模式由 SendMode 设置，后面有说明。

#### CoordMode

	CoordMode, ToolTip|Pixel|Mouse|Caret|Menu [, Screen|Window|Client]

**Param1**:

ToolTip: 作用于 ToolTip.

Pixel: 作用于 PixelGetColor, PixelSearch 和 ImageSearch.

Mouse: 作用于 MouseGetPos, Click 以及 MouseMove/Click/Drag.

Caret: 作用于内置变量 A_CaretX 和 A_CaretY.

Menu：作用于为 Menu Show 命令指定坐标的时候。

**Param2** (如果省略 Param2, 则默认为 Screen):

Screen: 坐标相对于桌面 (整个屏幕).

Relative: 坐标相对于活动窗口.

Window [v1.1.05+]: 与 Relative 效果相同, 但由于含义清晰, 因此建议使用.

Client [v1.1.05+]：坐标相对于活动窗口的工作区，其中不包括标题栏、菜单栏（如果它含有标准菜单栏）和边框。Client 坐标模式较少依赖于操作系统版本和主题.

#### SendMode

	SendMode Input|Play|Event|InputThenPlay

Event: 这是所有脚本开始时默认使用的. 它让 Send, SendRaw, Click 和 MouseMove/Click/Drag 使用 SendEvent 模式.

Input: 让 Send, SendRaw, Click 和 MouseMove/Click/Drag 切换到 SendInput 方法. 已知限制:

>Windows 资源管理器会忽略 SendInput 模拟的某些导航的热键, 例如 Alt+LeftArrow. 要变通解决此问题，请使用 SendEvent !{Left} 或 SendInput {Backspace}。

InputThenPlay [v1.0.43.02+]: 与上面相同, 不过当 SendInput 不可用 时恢复为下面的 Play 模式而不是退回到 Event 模式. 这也会使得 SendInput 命令 自身在 SendInput 不可用时恢复到 Play 模式.

Play: 让 Send, SendRaw, Click 和 MouseMove/Click/Drag 切换到 SendPlay 方法.


### ControlClick：

发送鼠标按钮或鼠标滚轮事件到控件。

	ControlClick [, Control-or-Pos, WinTitle, WinText, WhichButton, ClickCount, Options, ExcludeTitle, ExcludeText]

Control-or-Pos:

>如果此参数为空, 则点击目标窗口的顶层控件 (或如果窗口没有控件则点击窗口自身). 否则, 使用下列两种模式的其中一个.

模式 1 (位置): 指定相对于目标窗口左上角的 X 和 Y 坐标. X 坐标必须在 Y 坐标前面, 且它们之间需要含有至少一个空格或 tab. 例如：X55 Y33。如果在指定的坐标存在控件, 则会发送点击事件到这个坐标处. 如果没有控件, 则发送事件到目标窗口自身 (根据窗口的性质, 这可能不会产生效果). 注意：在此模式中，会忽略 Options 参数中的 X 和 Y 字母选项。

模式 2 (ClassNN 或文本): 可以指定 ClassNN (控件的类名和实例编号) 或控件的名称/文本, 它们都可以通过 Window Spy 获取. 使用名称/文本时, 匹配行为由 SetTitleMatchMode 决定.

WinTitle/WinText:

>选择窗口

Options:

>零个或多个下列选项字母组成的系列. 例如：d x50 y25。

NA [v1.0.45+]: 也许可以提高可靠性. 请参阅后面的 可靠性.

D: 按住鼠标按钮不放 (即生成按下事件). 如果 D 和 U 选项都没有包含, 则会发送完整的点击事件 (按下事件和弹起事件).

U: 释放鼠标按钮 (即生成弹起事件). 此选项不能和 D 选项同时使用.

Pos: 在 Options 的任意位置指定单词 Pos, 这样会无条件使用在上面 Control-or-Pos 参数中描述的 X/Y 位置模式.

Xn: 指定 n 为要点击的相对于控件左上角的 X 坐标. 如果未指定, 则在控件的水平中心点击.

Yn：指定 n 为要点击的相对于控件左上角的 Y 坐标。如果未指定, 则在控件的垂直中心点击.

在 X 和 Y 选项中使用十进制数而不是十六进制数.

ExcludeTitle/ExcludeText:

>排除窗口

	
### 其他函数
1.

	MouseClickDrag, WhichButton, X1, Y1, X2, Y2 [, Speed, R]

点击并按住指定的鼠标按钮，接着移动鼠标到目标坐标，然后松开按钮。

2.

	MouseMove, X, Y [, Speed, R]

Speed介于 0（最快）和 100（最慢）之间，可以为表达式，不设置的话为默认，见SetDefaultMouseSpeed

R:如果此参数为字母 R, 则会把 X 和 Y 坐标视为距离当前鼠标位置的偏移. 换句话说, 会把光标从当前位置往右移动 X 像素 (负值则往左) 且往下移动 Y 像素 (负值则往上).

3.

	MouseGetPos, [OutputVarX, OutputVarY, OutputVarWin, OutputVarControl, 1|2|3]

OutputVarX/Y用来保存 X 和 Y 坐标的变量名. 获取的坐标相对于活动窗口, 除非曾使用 CoordMode 改变成屏幕坐标.

OutputVarWin这个可选的参数是用来保存鼠标光标下窗口的 唯一 ID 号的变量名. 如果无法检测到此窗口, 则此变量被置空.即使窗口不处于活动状态, 也能检测到它的信息. 无法检测到隐藏窗口.

4.

	SetDefaultMouseSpeed, Speed

移动鼠标的速度，介于 0（最快）和 100（最慢）之间。注：速度为 0 表示瞬时移动鼠标到目标位置。此参数可以为 表达式.

在 SendInput/Play 模式 中会忽略 SetDefaultMouseSpeed; 它们会瞬时移动鼠标到目标位置


## 0x09 键盘控制

强制无条件安装键盘钩子。
	
	#InstallKeybdHook

### Send / SendRaw (Keys):

Keys表见 **0x11

SendRaw: 会原样发送所有字符, 而不把 {Enter} 转换成 ENTER 键击, 把 ^c 转换成 Control-C, 等等. 不过, 转义系列, 变量引用和表达式的一般规则仍然适用, 因为它们在命令执行前就已经被处理了. 要在 SendInput、SendPlay 或 SendEvent 中使用原始模式，请把 {Raw} 写在需发送的按键序列前面；例如：SendInput {Raw}abc。

Send: 不处于原始模式时, 下列字符被看成是修饰键 (这些修饰键仅影响紧跟着的下一个键):

>!: 发送 ALT 键击. 例如，Send This is text!a 将发送按键序列“This is text”并接着按下 ALT+a。注: 在某些程序中 !A 和 !a 会产生不同的效果. 这是由于 !A 按了 ALT+SHIFT+A 而 !a 按了 ALT+a. 如果不确定, 请使用小写字母.

>+: 发送 SHIFT 键击. 例如，Send +abC 会发送文本“AbC”，而 Send !+a 会按下 ALT+SHIFT+a。

>^: 发送 CONTROL 键击. 例如，Send ^!a 会按下 CTRL+ALT+a，而 Send ^{Home} 则发送 CONTROL+HOME。注: 在某些程序中 ^A 和 ^a 会产生不同的效果. 这是由于 ^A 按了 CONTROL+SHIFT+A 而 ^a 按了 CONTROL+a. 如果不确定, 请使用小写字母.

>#：发送 WIN 键击，因此 Send #e 会在按住 Windows 键时按下字母“e”。

### SendInput / SendPlay (Keys):

SendInput 和 SendPlay 与 Send 使用相同的语法但通常更快更可靠. 此外, 它们缓存了发送期间任何物理的键盘或鼠标活动, 这样避免了在发送时夹杂用户的键击. 可以使用 SendMode 让 Send 和 SendInput 或 SendPlay 执行相同的功能 

### 重复键击:

把需要重复的按键名称和重复次数写入到大括号中. 例如：

	Send {DEL 4}  ; 按 4 次 Delete 键.
	Send {S 30}   ; 发送 30 次大写字母 S.
	Send +{TAB 4}  ; 按 4 次 Shift-Tab.

### 按住或释放按键:

把按键名称和单词 Down 或 Up 写入到大括号中. 例如：

	Send {b down}{b up}
	Send {TAB down}{TAB up}
	Send {Up down}  ; 按下向上键.
	Sleep 1000  ; 按住 1 秒.
	Send {Up up}  ; 释放向上键.

## 0x0A 窗口管理



## 0x0B 屏幕管理



## 0x0C 文件管理 	
	


## 0x0D GUI绘制	



## 0x0E 声音管理


## 0x0F 内置函数


## 0x10 内置变量


## 0x11 键盘键值表
