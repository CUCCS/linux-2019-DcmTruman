# From GUI to CLI

## 实验要求

- 完成vimtutor内容，使用asciinema录像，并上传

## 实验结果

有些比较短，因为ng了好多次，想着尽可能流畅一些

mbp的touch bar上的esc键不是实体，按得难受，差评

### Lesson1

[![asciicast](https://asciinema.org/a/3LbnZjnrwgsZtV7ONRn60aZAK.svg)](https://asciinema.org/a/3LbnZjnrwgsZtV7ONRn60aZAK)

### Lesson2
[![asciicast](https://asciinema.org/a/A3QA6FIKWLi7QZiGrA5uqUqwH.svg)](https://asciinema.org/a/A3QA6FIKWLi7QZiGrA5uqUqwH)

### Lesson3
[![asciicast](https://asciinema.org/a/w41V1V67QY6bO5OktTX1dTR9a.svg)](https://asciinema.org/a/w41V1V67QY6bO5OktTX1dTR9a)

### Lesson4
[![asciicast](https://asciinema.org/a/951Knf9S1tR0mmewKv9HPVoAP.svg)](https://asciinema.org/a/951Knf9S1tR0mmewKv9HPVoAP)

### Lesson5
[![asciicast](https://asciinema.org/a/tH2Wz08LjjGxd6xTqQOYUW2FD.svg)](https://asciinema.org/a/tH2Wz08LjjGxd6xTqQOYUW2FD)

### Lesson6
[![asciicast](https://asciinema.org/a/i29TlXE19d4vlzUzOecT6GWeX.svg)](https://asciinema.org/a/i29TlXE19d4vlzUzOecT6GWeX)

### Lesson7
[![asciicast](https://asciinema.org/a/i29TlXE19d4vlzUzOecT6GWeX.svg)](https://asciinema.org/a/i29TlXE19d4vlzUzOecT6GWeX)

## FAQ

- 你了解vim有哪几种工作模式？
	- Normal mode 普通模式，打开文件初始位于该模式，其他模式下通过`Esc`键可以进入Normal 模式
	- Insert mode 插入模式，i,I,a,A,o,O,c等按键均可以进入Insert 模式
	- Visual mode 可视模式，带有选择高亮，普通模式下，按v，shift+v,ctrl+c均可以进入Visual 模式
- Normal模式下，从当前行开始，一次向下移动光标10行的操作方法？如何快速移动到文件开始行和结束行？如何快速跳转到文件中的第N行？
	- `10j`
	- 文件开始 ： `gg`,文件结束：`G`
	- 行数gg或者行数G，比如跳到100行，按100G或100gg
- Normal模式下，如何删除单个字符、单个单词、从当前光标位置一直删除到行尾、单行、当前行开始向下数N行？
	- `x`删除单个字符
	- 光标在单词头，`dw`或者`de`删除单个单词
	- `d$`删到尾
	- `dd`删除一行
	- `行数dd`，删除N行
- 如何在vim中快速插入N个空行？如何在vim中快速输入80个-？
	- `[N]o` 向下插入80个空行
	- `[N]i-` 快速插入80个-
- 如何撤销最近一次编辑操作？如何重做最近一次被撤销的操作？
	- 撤销最近一次操作 ： `u`
	- 重做最近一次撤销 ： `ctrl+r`
- vim中如何实现剪切粘贴单个字符？单个单词？单行？如何实现相似的复制粘贴操作呢？
	- vim中，最近一次删除的内容会在vim的剪切板中保留，功能类似于剪切，粘贴只需要按`p`即可
	- `yy`复制一行，`[N]yy`复制N行，`yw`复制单个单词，`y`复制visual mode中选定的某一块
- 为了编辑一段文本你能想到哪几种操作方式（按键序列）？
	- `h,j,k,l,w,b,0,$` : 光标操作
	- `/[search]`:查询
	- `ctrl d,ctrl u`:上/下翻半页
	- `i,I,o,O,a,A`基本插入操作
	- `dd,d`:删除
	- `:x`:保存并退出
- 查看当前正在编辑的文件名的方法？查看当前光标所在行的行号的方法？
	- `ctrl + g`
- 在文件中进行关键词搜索你会哪些方法？如何设置忽略大小写的情况下进行匹配搜索？如何将匹配的搜索结果进行高亮显示？如何对匹配到的关键词进行批量替换？
	- /[关键字|匹配模式]，`n`下一个，`N`上一个
	- `set ic` ,忽略大小写
	- `set hlsearch`,结果高亮
	- 全局：`:%s/old/new/g`,x行到y行：`:x,y/old/new/g`


- 在文件中最近编辑过的位置来回快速跳转的方法？
	- `ctrl + o`,`ctrl + i`

- 如何把光标定位到各种括号的匹配项？例如：找到(, [, or {对应匹配的),], or }
	- 光标一到某个括号，按`%`，即可到他对应的括号

- 在不退出vim的情况下执行一个外部程序的方法？
	- `![程序]`
- 如何使用vim的内置帮助系统来查询一个内置默认快捷键的使用方法？如何在两个不同的分屏窗口中移动光标？
	- 查询一个内置默认快捷键的使用方法 :`:help [快捷键]`
	- :set mouse=a,然后可以通过鼠标操作光标在不同窗口
	- `ctrl + w + h/j/k/l`,通过键盘移动光标到不同窗口


