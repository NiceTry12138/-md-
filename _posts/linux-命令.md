---
title: 作死的学习Linux运维
date: 2018-10-27 16:07:26
tags:
---


## Linux命令行

大多是互联网企业在安装系统甚至不会安装图形管理软件包，而是直接使用文本模式安装，因此登陆后直接面对的就是命令行的界面

### Linux命令行提示符介绍

Linux命令行结尾的提示符有 "#" 和 "$" 两种不同的符号  

	# 是超级管理员root用户对应的命令行 
	$ 是普通用户oldboy对应的命令行

### 命令行的快捷键

```shell
tab				命令或路径等的补全键，Linux最有用的快捷键
Ctrl+a			光标回到命令行行首
Ctrl+e			光标回到命令行行尾
Ctrl+f			光标向右移动一个字符（相当于方向键右键）
Ctrl+b			光标向左移动一个字符（相当于方向键左键）
Ctrl+insert		复制命令行内容
shift+insert	粘贴命令行内容
Ctrl+k			剪切（删除）光标处到行尾的字符
Ctrl+u			剪切（删除）光标处到行首的字符
Ctrl+w			剪切（删除）光标钱的一个单词
Ctrl+y			粘贴上面三个剪贴的内容
Ctrl+c			中断终端正在执行的任务或者删除整行
!!				执行上一条命令
!pw				执行最近以pw开头的命令
!pw:p			仅打印最近以pw开头的命令，不执行
!num			执行历史命令列表的第num条命令
!$				上一条命令的最后一个参数
Esc+.			获取上一条命令最后的部分
Esc+b			移动到当前单词的开头
Esc+f			移动到当前单词的结尾
```

### Linux命令行下查看命令帮助

#### man命令

man命令是Linux系统中最核心的命令之一，因为通过它可以查看其他linux命令的使用信息，当然还可以查看软件的配置文件、系统调用、库函数等的帮助信息

##### 语法格式
	man 参数选项 命令/文件

###### 参数选项

<table>
<tr>
<td>数字参数</td><td>说明</td><td>解释说明</td>
</tr>
<tr>
<td>1</td><td>User Commands</td><td>用户命令相关</td>
</tr>
<tr>
<td>2</td><td>System Calls</td><td>系统调用相关</td>
</tr>
<tr>
<td>3</td><td>C Library Functions</td><td>C的库函数相关</td>
</tr>
<tr>
<td>4</td><td>Devices and Special Files</td><td>设备和特殊文件相关</td>
</tr>
<tr>
<td>5</td><td>File Formats and Conventions</td><td>文件格式和规则</td>
</tr>
<tr>
<td>6</td><td>Games et. AI.</td><td>游戏及其他</td>
</tr>
<tr>
<td>7</td><td>Miscellanea</td><td>宏，包，及其他杂项</td>
</tr>
<tr>
<td>8</td><td>System Administration tools and Deamons</td><td>系统管理员命令和进程</td>
</tr>
</table>

##### 查阅的内容格式

<table>
<tr>
<td>man帮助信息中的标题</td><td>功能说明</td>
</tr>
<tr>
<td>NAME</td><td>命令说明介绍</td>
</tr>
<tr>
<td>SYNOPSIS</td><td>命令的基本使用语法</td>
</tr>
<tr>
<td>DESCRIPTION</td><td>命令行使用详细描述，以及相关参数选项说明</td>
</tr>
<tr>
<td>OPTION</td><td>命令相关参数选项说明</td>
</tr>
<tr>
<td>COMMANDS</td><td>在执行这个程序的时候，可以在此程序中执行的命令</td>
</tr>
<tr>
<td>FILES</td><td>程序涉及的相关文件</td>
</tr>
<tr>
<td>EXAMPLES</td><td>命令的一些例子</td>
</tr>
<tr>
<td>SEE ALSO</td><td>和命令相关的信息说明</td>
</tr>
<tr>
<td>BUGS（REPORTIONG BUGS）</td><td>命令对应缺陷问题的描述</td>
</tr>
<tr>
<td>COPYRIGHT</td><td>坂玄信息相关声明</td>
</tr>
<tr>
<td>AUTHOR</td><td>作者介绍</td>
</tr>
</table>


#### --help获取命令帮助

使用起来很简单啦，就是 " 命令 --help "

##### 使用方法
	--help 获取的是常用的帮助信息， man命令获取的是更过更复杂的帮助信息
	例如：
		mv --help

#### help获取bash内置命令

在Linux系统里有一些特殊的命令，他们就是bash程序的内置命令，例如：cd，ls......
这些命令并不存在真实的程序文件，对于这些命令，查看帮助的方式就是使用help

##### 使用方法
	help 命令
	例如：
		help cd

#### info获取帮助信息

Linux系统中的info命令是一个查看程序对应文档的命令，可以作为man及help命令的帮助补充，用的少

##### 使用方法
	info 命令
	例如：
		info ls

#### 从互联网获取命令帮助信息
	简单一条 百度，google，总之怎么快怎么来。

![](https://i.imgur.com/wrkAmPX.jpg)


### Linux的关机，重启，注销命令

#### shutdown命令

##### 使用方法及例子
	shutdown [OPTION]... TIME[MESSAFE]
	shutdown [选项] 时间 信息
	通常形况下，一般用的比较多的就是 shutdown -h now 或者 shutdown -r now
	例子：
		shutdown -h +1		#一分钟后关机
		shutdown -r 11:00	#十一点关机

<table>
<tr>
<td>参数选项</td><td>解释说明</td>
</tr>
<tr>
<td>-r</td><td>重启系统，而不是关机</td>
</tr>
<tr>
<td>-h</td><td>关机</td>
</tr>
<tr>
<td>-H</td><td>关机，但是并不是完全关机，不常用</td>
</tr>
<tr>
<td>-P</td><td>关机，不常用</td>
</tr>
<tr>
<td>-c</td><td>取消正在执行的shutdown命令</td>
</tr>
<tr>
<td>-k</td><td>只发送关机提示，但是并不关机，就闹着玩玩</td>
</tr>
</table>
​	

##### 工作原理

shutdown命令的工作原理为：一旦到达关机时间，shutdown命令就会发送请求给系统的init进程将系统调整到合适的运行级别（运行级别请参考runlevel命令，运行级别请查看/etc/inittab文件说明），其中0表示关机，6表示重启。所以，执行 "init 0"就表示关机，执行"init 6"表示重启



#### halt/poweroff/reboot 重启关机命令

##### 语法格式
	reboot [OPTION]...
	halt [OPTION]...
	poweroff [OPTION]...
	通常情况下，执行这三个命令不带任何参数

##### 使用
	halt 		#就是直接关机
	reboot 		#就是直接重启
	poweroff	#就是直接关机


#### 一些常见的关机，重启，注销命令

<table>
<tr>
<td>命令</td><td>说明</td>
</tr>
<tr>
<td>shutdown -h now</td><td>立刻关机</td>
</tr>
<tr>
<td>shutdwn -h +1</td><td>一分钟后关机，+1也可以是时间点，例如：11：00</td>
</tr>
<tr>
<td>halt</td><td>立刻停止系统，需要人工关闭电源</td>
</tr>
<tr>
<td>init 0</td><td>切换运行级别到0，关机</td>
</tr>
<tr>
<td>poweroff</td><td>立刻停止系统，并且关闭电源</td>
</tr>
<tr>
<td>reboot</td><td>立刻重启</td>
</tr>
<tr>
<td>shutdown -r now</td><td>立刻重启</td>
</tr>
<tr>
<td>shutdown -r +1</td><td>一分钟后重启</td>
</tr>
<tr>
<td>init 6</td><td>切换运行级别到6，重启</td>
</tr>
<tr>
<td>logout</td><td>注销退出当前用户</td>
</tr>
<tr>
<td>exit</td><td>注销退出当前用户窗口</td>
</tr>
</table>

## 文件和目录操作命令

### pwd 显示当前所在的位置

#### 命令详解
	pwd命令是 "print working directory"中每个单词的首字母缩写，其功能是显示当前工作目录的绝对路径。

#### 语法格式
	pwd [option]
	pwd [选项]

#### 选项说明

<table>
<tr>
<td>参数选项</td><td>解释说明</td>
</tr>
<tr>
<td>-L</td><td>logical首字母缩写，表示显示逻辑路径，取PWD系统环境变量的值</td>
</tr>
<tr>
<td>-P</td><td>physical首字符缩写，表示显示物理路径时如果当前目录路径是软链接文件，则会显示软链接文件对应的源文件</td>
</tr>
</table>

	查看命令帮助时，我们经常会看到 "-L,--logical" 这样的选项格式，这种写法的意思是 -L 和 --logical 的功能是一样的。

#### 高级范例

为什么管理员会用到pwd命令呢？
这是因为我们通过命令行管理Linux时，经常会切换到不同的路径，而输入pwd命令可以随时查看当前的路径是什么。  
其实，在喜荣忠使用Bash命令行就会自动显示用户当前所在的路径，但是默认情况下这种路径显示不全。  

当然可以通过修改PS1对应的值来改变；
#### 修改PS1

<table>
<tr>
<td>PS1</td><td>含义</td>
</tr>
<tr>
<td>\d</td><td>代表日期，格式为 weekday month date</td>
</tr>
<tr>
<td>\H</td><td>完整的主机名称</td>
</tr>
<tr>
<td>\h</td><td>仅取主机的第一个名字</td>
</tr>
<tr>
<td>\t</td><td>显示时间为24小时格式，如：HH：MM：SS</td>
</tr>
<tr>
<td>\T</td><td>显示时间为12小时格式</td>
</tr>
<tr>
<td>\A</td><td>显示时间为24小时格式，如：HH：MM</td>
</tr>
<tr>
<td>\u</td><td>当前用户的账号信息</td>
</tr>
<tr>
<td>\v</td><td>BASH的版本信息</td>
</tr>
<tr>
<td>\w</td><td>显示完整的路径，其中家目录会以~替代</td>
</tr>
<tr>
<td>\W</td><td>利用basename取得工作目录名称，所以只会列出最后一个目录</td>
</tr>
<tr>
<td>\#</td><td>执行的第几条命令</td>
</tr>
<tr>
<td>\$</td><td>提示字符，root用户为#，否则为$</td>
</tr>
</table>

	因此，要查看当前PS1变量的值，可采用如下命令：
		echo $PS1		#打印超级管理员对应的PS1值
		打印出：[\u@\u \W]\$		#  @时一个分隔符，和邮箱地址中的@作用类似
	
	修改PS1变量对应的值：
		PS1='[\u@\h \w]'	#此命令仅临时生效
		编辑 /etc/bashrc 文件，找到这个语句 ["$PS1"="\\s-\\v\\\$"]&&PS1="[\u@\h \W]\\$"
		修改为：["$PS1"="\\s-\\v\\\$"]&&PS1="[\u@\h \w]\\$"
	最后注销重启就行了

### cd 切换目录

#### 功能说明
	cd命令时 "change direcotry"中每个单词的首字母缩写，其功能时从当前工作目录切换到制定的工作目录

#### 语法格式
	cd [option] [dir]
	cd [选项] [目录]

<table>
<tr>
<td>参数选项</td><td>解释说明</td>
</tr>
<tr>
<td>-P</td><td>如果切换的目标目录是一个软链接，则会直接切换到软链接指向的真正物理目标目录，和pwd命令的-P选项功能类似</td>
</tr>
<tr>
<td>-L</td><td>功能与-P相反，如果切换的目标目录是一个软连接，则直接切换到软链接所在的目录</td>
</tr>
<tr>
<td>-</td><td>当只使用"-"选项时，将会从当前目录切换到系统环境变量"OLDPWD"对应值的目录路径</td>
</tr>
<tr>
<td>~</td><td>当只是用"~"选项时，将会从当前目录切换到系统环境变量"HOME"对应值的目录路径</td>
</tr>
<tr>
<td>..</td><td>当只是用".."选项时，将会从当前目录切换到当前目录的上一级目录所在的路径</td>
</tr>
</table>

#### 使用范例

- cd /etc		进入系统etc目录
- cd ..			返回上一级目录
- cd ../../		退回当前目录的上两级目录
- cd ~			切换到家目录
- cd -			返回当前用户上一次所在的目录

### mkdir创建目录

- mkdir命令是"make directories"中每个单词的字母组成，其功能是创建目录，默认情况下要创建的目录已存在，则会报错。

#### 语法格式
	mkdir [optioin] [directory]
	mkdir [选项] [目录]
	
	mkdir 可以同时创建多个目录，格式为 mkdir dir1 dir2 dir3 ...

#### 选项说明

<table>
<tr>
<td>参数选项</td><td>解释说明</td>
</tr>
<tr>
<td>-p</td><td>递归创建目录，即使要创建的目录已经存在也不会报错提示目录存在</td>
</tr>
<tr>
<td>-m</td><td>设置新创建目录的默认目录对应的权限</td>
</tr>
<tr>
<td>-v</td><td>显示创建目录的过程</td>
</tr>
</table>

#### 例子

- mkdir data 			#创建data文件夹
- mkdir oldboy/test		#创建oldboy文件夹并在oldboy目录下创建test目录
- mkdir -pv oldboy1/test#创建oldboy目录并在oldboy目录下创建test目录，同时显示过程
- mkdir -m 333 dir2		#创建dir2目录，并且设置权限为333
- mkdir -pv oldboy/{dir1_1,dir1_2}/{dir2_1, dir2_2}...
	- 解释：
	- mkdir: created direcory 'oldboy/dir1_1'
	- mkdir: created direcory 'oldboy/dir1_1/dir2_1'
	- mkdir: created direcory 'oldboy/dir1_1/dir2_2'
	- mkdir: created direcory 'oldboy/dir1_2'
	- mkdir: created direcory 'oldboy/dir1_2/dir2_1'
	- mkdir: created direcory 'oldboy/dir1_2/dir2_2'


### touch 创建空文件或改变文件的时间戳属性

- touch 有两个功能
	- 创建新的空文件
	- 改变已有文件的时间戳属性

#### 语法格式
	touch [optioini] [file]
	touch [选项]	[文件]

- touch 是创建空的文件， mkdir 是创建空的目录，是不一样的

#### 选项说明
<table>
<tr>
<td>参数选项</td><td>解释说明</td>
</tr>
<tr>
<td>-a</td><td>只更改指定文件的最后访问时间</td>
</tr>
<tr>
<td>-d STRING</td><td>使用字符串STRING代表的时间作为模板设置指定文件的时间属性</td>
</tr>
<tr>
<td>-m</td><td>只更改指定文件的最后修改时间</td>
</tr>
<tr>
<td>-r file</td><td>将指定问及爱你的时间属性这是为与模板文件file的时间属性相同</td>
</tr>
<tr>
<td>-t STAMP</td><td>使用[[CC]YY]MMDDhhmm[.ss]格式的时间设置文件的时间属性，从左到右依次是：世纪，年，月，日，时，分，秒</td>
</tr>
</table>

#### 使用范例
- touch test.txt			#创建空的文件test.txt
- touch a.txt b.txt 		#同时创建多个文件
- touch stu{01..05}.txt		#同时创建01~05文件
- stat test.txt				#用stat命令查看文件是时间戳属性
- touch test.txt			#更改最后的修改的时间为当前时间
- touch -d 20201001 test.txt#修改时间更改为2020年
- touch -r a.txt test.txt	#修改test.txt的时间属性与a.txt时间属性一致

#### 时间戳形式
- stat命令对应的时间戳
	- Access: 	最后访问时间
	- Modify:	最后修改文件时间
	- Change:	最后改变文件状态的时间

- ls命令对应的时间戳
	- mtime:	最后修改时间(ls -lt)
	- ctime:	状态改变时间(ls -lc)
	- atime:	最后访问时间(ls -lu)

### ls 显示目录下的内容及相关属性

- ls命令可以理解为英文单词list的缩写，其功能是列出列表的内容及其内容属性

#### 语法格式
	ls [option] [file]
	ls [选项] [<文件或目录>]

#### 选项说明
<table>
<tr>
<td>参数选项</td><td>解释说明</td>
</tr>
<tr>
<td>-l</td><td>使用长格式列出文件及目录信息</td>
</tr>
<tr>
<td>-a</td><td>显示目录下的所有文件，包括以'.'字符开始的隐藏文件</td>
</tr>
<tr>
<td>-t</td><td>根据最后的修改时间(mtime)排序，默认是按文件名排序</td>
</tr>
<tr>
<td>-r</td><td>以相反次序排序</td>
</tr>
<tr>
<td>-F</td><td>在条目后加上文件类型的只是符号(*,.,=,@,|中的一个)</td>
</tr>
<tr>
<td>-p</td><td>直在目录后面加上 '/'</td>
</tr>
<tr>
<td>-i</td><td>显示inode节点信息</td>
</tr>
<tr>
<td>-d</td><td>当遇到目录时，列出目录本身而非目录内的文件，并不跟随符号链接</td>
</tr>
<tr>
<td>-h</td><td>以人类可读的信息显示文件或目录大小</td>
</tr>
<tr>
<td>-A</td><td>列出所有文件，包括隐藏文件，但不包括'.''..'</td>
</tr>
<tr>
<td>-S</td><td>根据文件大小排序</td>
</tr>
<tr>
<td>-R</td><td>递归列数所有子目录</td>
</tr>
<tr>
<td>-x</td><td>逐行列出项目而不是逐栏列出</td>
</tr>
<tr>
<td>-X</td><td>根据扩展名排序</td>
</tr>
<tr>
<td>-c</td><td>根据状态改变时间排序(ctime)</td>
</tr>
<tr>
<td>-u</td><td>根据最后访问时间排序(atime)</td>
</tr>
<tr>
<td>-color={never,always,auto}</td><td>不同的文件类型显示不同的颜色参数，never不现实，auto自动，always总是显示</td>
</tr>
<tr>
<td>--full-time</td><td>以完整的时间格式输出</td>
</tr>
<tr>
<td>--time-style={full-iso,long-iso,iso,local}</td><td>以不同的时间格式输出，long-iso效果最好</td>
</tr>
<tr>
<td>--time={atime,ctiom}</td><td>按不同的时间属性输出</td>
</tr>
</table>

#### 使用范例

- ls				#不带参数
- ls -a				#显示'.'
- ls -A				#显示所有文件，包括隐藏文件
- ls -l				#长格式输出文件类型，权限，链接数，属组，时间等
- ls -l --time-style=long-iso #以long-iso方式显示时间
- ls -F				#显示文件，文件夹后加上'/'
- 当然你也可以用alias方法给原本很长ls命令取个别名
	- alias lst='ls -l --time-style=long-iso'
		- 给 ls -l --time-style=long-iso 起别名为 lst
- ls -F				#给文件夹后加上'/'，其他文件加上其他字符
	- '*'	可执行的普通文件
	- '/'	目录
	- '='	套接字(sockets)
	- '|'	FIFOS
	- '@'	符号链接

- ls -lhi
	- 命令对应列数意义
	- 第一列：	inode索引节点的编号
	- 第二列:	文件类型及权限
	- 第三列：	硬连接个数
	- 第四列:	文件或目录所属的用户
	- 第五列：	文件或目录所属的组
	- 第六列：	文件或目录的大小
	- 第七，八，九列：	文件或目录的修改时间
	- 第十列：	实际的文件名或目录名

### cp 复制文件或目录

- cp命令可以理解为英文单词copy的缩写，其功能为复制文件或目录

#### 语法格式
	cp [option] [source] [dest]
	cp [选项] [源文件] [目标文件]

#### 选项说明

<table>
<tr>
<td>参数选项</td><td>解释说明</td>
</tr>
<tr>
<td>-p</td><td>复制文件时保持源文件的所有者，权限信息及时间属性</td>
</tr>
<tr>
<td>-d</td><td>如果复制的源文件是符号链接，那么仅复制链接本身，而且保留符号链接所指向的目标文件或目录</td>
</tr>
<tr>
<td>-r</td><td>递归复制目录，即复制目录下的所有层级的子目录及文件</td>
</tr>
<tr>
<td>-a</td><td>等同于上面的p,d,r这三个选项功能的综合</td>
</tr>
<tr>
<td>-i</td><td>覆盖已有文件前提示用户确认</td>
</tr>
<tr>
<td>-t</td><td>默认情况下命令格式是 'cp源文件 目标文件'，使用-t后变成 'cp 目标文件 源文件'</td>
</tr>
</table>

#### 使用范例

- cp -i test.file file1.test

## 系统信息 
	arch 显示机器的处理器架构(1) 
	uname -m 显示机器的处理器架构(2) 
	uname -r 显示正在使用的内核版本 
	dmidecode -q 显示硬件系统部件 - (SMBIOS / DMI) 
	hdparm -i /dev/hda 罗列一个磁盘的架构特性 
	hdparm -tT /dev/sda 在磁盘上执行测试性读取操作 
	cat /proc/cpuinfo 显示CPU info的信息 
	cat /proc/interrupts 显示中断 
	cat /proc/meminfo 校验内存使用 
	cat /proc/swaps 显示哪些swap被使用 
	cat /proc/version 显示内核的版本 
	cat /proc/net/dev 显示网络适配器及统计 
	cat /proc/mounts 显示已加载的文件系统 
	lspci -tv 罗列 PCI 设备 
	lsusb -tv 显示 USB 设备 
	date 显示系统日期 
	cal 2007 显示2007年的日历表 
	date 041217002007.00 设置日期和时间 - 月日时分年.秒 
	clock -w 将时间修改保存到 BIOS 



## 文件和目录 
	cd /home 进入 '/ home' 目录' 
	cd .. 返回上一级目录 
	cd ../.. 返回上两级目录 
	cd 进入个人的主目录 
	cd ~user1 进入个人的主目录 
	cd - 返回上次所在的目录 
	pwd 显示工作路径 
	ls 查看目录中的文件 
	ls -F 查看目录中的文件 
	ls -l 显示文件和目录的详细资料 
	ls -a 显示隐藏文件 
	ls *[0-9]* 显示包含数字的文件名和目录名 
	tree 显示文件和目录由根目录开始的树形结构(1) 
	lstree 显示文件和目录由根目录开始的树形结构(2) 
	mkdir dir1 创建一个叫做 'dir1' 的目录' 
	mkdir dir1 dir2 同时创建两个目录 
	mkdir -p /tmp/dir1/dir2 创建一个目录树 
	rm -f file1 删除一个叫做 'file1' 的文件' 
	rmdir dir1 删除一个叫做 'dir1' 的目录' 
	rm -rf dir1 删除一个叫做 'dir1' 的目录并同时删除其内容 
	rm -rf dir1 dir2 同时删除两个目录及它们的内容 
	mv dir1 new_dir 重命名/移动 一个目录 
	cp file1 file2 复制一个文件 
	cp dir/* . 复制一个目录下的所有文件到当前工作目录 
	cp -a /tmp/dir1 . 复制一个目录到当前工作目录 
	cp -a dir1 dir2 复制一个目录 
	ln -s file1 lnk1 创建一个指向文件或目录的软链接 
	ln file1 lnk1 创建一个指向文件或目录的物理链接 
	touch -t 0712250000 file1 修改一个文件或目录的时间戳 - (YYMMDDhhmm) 
	file file1 outputs the mime type of the file as text 
	iconv -l 列出已知的编码 
	iconv -f fromEncoding -t toEncoding inputFile > outputFile creates a new from the given input file by assuming it is encoded in fromEncoding and converting it to toEncoding. 
	find . -maxdepth 1 -name *.jpg -print -exec convert "{}" -resize 80x60 "thumbs/{}" \; batch resize files in the current directory and send them to a thumbnails directory (requires convert from Imagemagick) 



## 文件搜索 
	find / -name file1 从 '/' 开始进入根文件系统搜索文件和目录 
	find / -user user1 搜索属于用户 'user1' 的文件和目录 
	find /home/user1 -name \*.bin 在目录 '/ home/user1' 中搜索带有'.bin' 结尾的文件 
	find /usr/bin -type f -atime +100 搜索在过去100天内未被使用过的执行文件 
	find /usr/bin -type f -mtime -10 搜索在10天内被创建或者修改过的文件 
	find / -name \*.rpm -exec chmod 755 '{}' \; 搜索以 '.rpm' 结尾的文件并定义其权限 
	find / -xdev -name \*.rpm 搜索以 '.rpm' 结尾的文件，忽略光驱、捷盘等可移动设备 
	locate \*.ps 寻找以 '.ps' 结尾的文件 - 先运行 'updatedb' 命令 
	whereis halt 显示一个二进制文件、源码或man的位置 
	which halt 显示一个二进制文件或可执行文件的完整路径 



## 挂载一个文件系统 
	mount /dev/hda2 /mnt/hda2 挂载一个叫做hda2的盘 - 确定目录 '/ mnt/hda2' 已经存在 
	umount /dev/hda2 卸载一个叫做hda2的盘 - 先从挂载点 '/ mnt/hda2' 退出 
	fuser -km /mnt/hda2 当设备繁忙时强制卸载 
	umount -n /mnt/hda2 运行卸载操作而不写入 /etc/mtab 文件- 当文件为只读或当磁盘写满时非常有用 
	mount /dev/fd0 /mnt/floppy 挂载一个软盘 
	mount /dev/cdrom /mnt/cdrom 挂载一个cdrom或dvdrom 
	mount /dev/hdc /mnt/cdrecorder 挂载一个cdrw或dvdrom 
	mount /dev/hdb /mnt/cdrecorder 挂载一个cdrw或dvdrom 
	mount -o loop file.iso /mnt/cdrom 挂载一个文件或ISO镜像文件 
	mount -t vfat /dev/hda5 /mnt/hda5 挂载一个Windows FAT32文件系统 
	mount /dev/sda1 /mnt/usbdisk 挂载一个usb 捷盘或闪存设备 
	mount -t smbfs -o username=user,password=pass //WinClient/share /mnt/share 挂载一个windows网络共享 



## 磁盘空间 
	df -h 显示已经挂载的分区列表 
	ls -lSr |more 以尺寸大小排列文件和目录 
	du -sh dir1 估算目录 'dir1' 已经使用的磁盘空间' 
	du -sk * | sort -rn 以容量大小为依据依次显示文件和目录的大小 
	rpm -q -a --qf '%10{SIZE}t%{NAME}n' | sort -k1,1n 以大小为依据依次显示已安装的rpm包所使用的空间 (fedora, redhat类系统) 
	dpkg-query -W -f='${Installed-Size;10}t${Package}n' | sort -k1,1n 以大小为依据显示已安装的deb包所使用的空间 (ubuntu, debian类系统) 



## 用户和群组 
	groupadd group_name 创建一个新用户组 
	groupdel group_name 删除一个用户组 
	groupmod -n new_group_name old_group_name 重命名一个用户组 
	useradd -c "Name Surname " -g admin -d /home/user1 -s /bin/bash user1 创建一个属于 "admin" 用户组的用户 
	useradd user1 创建一个新用户 
	userdel -r user1 删除一个用户 ( '-r' 排除主目录) 
	usermod -c "User FTP" -g system -d /ftp/user1 -s /bin/nologin user1 修改用户属性 
	passwd 修改口令 
	passwd user1 修改一个用户的口令 (只允许root执行) 
	chage -E 2005-12-31 user1 设置用户口令的失效期限 
	pwck 检查 '/etc/passwd' 的文件格式和语法修正以及存在的用户 
	grpck 检查 '/etc/passwd' 的文件格式和语法修正以及存在的群组 
	newgrp group_name 登陆进一个新的群组以改变新创建文件的预设群组 



## 文件的权限 - 使用 "+" 设置权限，使用 "-" 用于取消 
	ls -lh 显示权限 
	ls /tmp | pr -T5 -W$COLUMNS 将终端划分成5栏显示 
	chmod ugo+rwx directory1 设置目录的所有人(u)、群组(g)以及其他人(o)以读（r ）、写(w)和执行(x)的权限 
	chmod go-rwx directory1 删除群组(g)与其他人(o)对目录的读写执行权限 
	chown user1 file1 改变一个文件的所有人属性 
	chown -R user1 directory1 改变一个目录的所有人属性并同时改变改目录下所有文件的属性 
	chgrp group1 file1 改变文件的群组 
	chown user1:group1 file1 改变一个文件的所有人和群组属性 
	find / -perm -u+s 罗列一个系统中所有使用了SUID控制的文件 
	chmod u+s /bin/file1 设置一个二进制文件的 SUID 位 - 运行该文件的用户也被赋予和所有者同样的权限 
	chmod u-s /bin/file1 禁用一个二进制文件的 SUID位 
	chmod g+s /home/public 设置一个目录的SGID 位 - 类似SUID ，不过这是针对目录的 
	chmod g-s /home/public 禁用一个目录的 SGID 位 
	chmod o+t /home/public 设置一个文件的 STIKY 位 - 只允许合法所有人删除文件 
	chmod o-t /home/public 禁用一个目录的 STIKY 位 



## 文件的特殊属性 - 使用 "+" 设置权限，使用 "-" 用于取消 
	chattr +a file1 只允许以追加方式读写文件 
	chattr +c file1 允许这个文件能被内核自动压缩/解压 
	chattr +d file1 在进行文件系统备份时，dump程序将忽略这个文件 
	chattr +i file1 设置成不可变的文件，不能被删除、修改、重命名或者链接 
	chattr +s file1 允许一个文件被安全地删除 
	chattr +S file1 一旦应用程序对这个文件执行了写操作，使系统立刻把修改的结果写到磁盘 
	chattr +u file1 若文件被删除，系统会允许你在以后恢复这个被删除的文件 
	lsattr 显示特殊的属性 



## 打包和压缩文件 
	bunzip2 file1.bz2 解压一个叫做 'file1.bz2'的文件 
	bzip2 file1 压缩一个叫做 'file1' 的文件 
	gunzip file1.gz 解压一个叫做 'file1.gz'的文件 
	gzip file1 压缩一个叫做 'file1'的文件 
	gzip -9 file1 最大程度压缩 
	rar a file1.rar test_file 创建一个叫做 'file1.rar' 的包 
	rar a file1.rar file1 file2 dir1 同时压缩 'file1', 'file2' 以及目录 'dir1' 
	rar x file1.rar 解压rar包 
	unrar x file1.rar 解压rar包 
	tar -cvf archive.tar file1 创建一个非压缩的 tarball 
	tar -cvf archive.tar file1 file2 dir1 创建一个包含了 'file1', 'file2' 以及 'dir1'的档案文件 
	tar -tf archive.tar 显示一个包中的内容 
	tar -xvf archive.tar 释放一个包 
	tar -xvf archive.tar -C /tmp 将压缩包释放到 /tmp目录下 
	tar -cvfj archive.tar.bz2 dir1 创建一个bzip2格式的压缩包 
	tar -jxvf archive.tar.bz2 解压一个bzip2格式的压缩包 
	tar -cvfz archive.tar.gz dir1 创建一个gzip格式的压缩包 
	tar -zxvf archive.tar.gz 解压一个gzip格式的压缩包 
	zip file1.zip file1 创建一个zip格式的压缩包 
	zip -r file1.zip file1 file2 dir1 将几个文件和目录同时压缩成一个zip格式的压缩包 
	unzip file1.zip 解压一个zip格式压缩包 



## RPM 包 - （Fedora, Redhat及类似系统） 
	rpm -ivh package.rpm 安装一个rpm包 
	rpm -ivh --nodeeps package.rpm 安装一个rpm包而忽略依赖关系警告 
	rpm -U package.rpm 更新一个rpm包但不改变其配置文件 
	rpm -F package.rpm 更新一个确定已经安装的rpm包 
	rpm -e package_name.rpm 删除一个rpm包 
	rpm -qa 显示系统中所有已经安装的rpm包 
	rpm -qa | grep httpd 显示所有名称中包含 "httpd" 字样的rpm包 
	rpm -qi package_name 获取一个已安装包的特殊信息 
	rpm -qg "System Environment/Daemons" 显示一个组件的rpm包 
	rpm -ql package_name 显示一个已经安装的rpm包提供的文件列表 
	rpm -qc package_name 显示一个已经安装的rpm包提供的配置文件列表 
	rpm -q package_name --whatrequires 显示与一个rpm包存在依赖关系的列表 
	rpm -q package_name --whatprovides 显示一个rpm包所占的体积 
	rpm -q package_name --scripts 显示在安装/删除期间所执行的脚本l 
	rpm -q package_name --changelog 显示一个rpm包的修改历史 
	rpm -qf /etc/httpd/conf/httpd.conf 确认所给的文件由哪个rpm包所提供 
	rpm -qp package.rpm -l 显示由一个尚未安装的rpm包提供的文件列表 
	rpm --import /media/cdrom/RPM-GPG-KEY 导入公钥数字证书 
	rpm --checksig package.rpm 确认一个rpm包的完整性 
	rpm -qa gpg-pubkey 确认已安装的所有rpm包的完整性 
	rpm -V package_name 检查文件尺寸、 许可、类型、所有者、群组、MD5检查以及最后修改时间 
	rpm -Va 检查系统中所有已安装的rpm包- 小心使用 
	rpm -Vp package.rpm 确认一个rpm包还未安装 
	rpm2cpio package.rpm | cpio --extract --make-directories *bin* 从一个rpm包运行可执行文件 
	rpm -ivh /usr/src/redhat/RPMS/`arch`/package.rpm 从一个rpm源码安装一个构建好的包 
	rpmbuild --rebuild package_name.src.rpm 从一个rpm源码构建一个 rpm 包 



## YUM 软件包升级器 - （Fedora, RedHat及类似系统） 
	yum install package_name 下载并安装一个rpm包 
	yum localinstall package_name.rpm 将安装一个rpm包，使用你自己的软件仓库为你解决所有依赖关系 
	yum update package_name.rpm 更新当前系统中所有安装的rpm包 
	yum update package_name 更新一个rpm包 
	yum remove package_name 删除一个rpm包 
	yum list 列出当前系统中安装的所有包 
	yum search package_name 在rpm仓库中搜寻软件包 
	yum clean packages 清理rpm缓存删除下载的包 
	yum clean headers 删除所有头文件 
	yum clean all 删除所有缓存的包和头文件 



## DEB 包 (Debian, Ubuntu 以及类似系统) 
	dpkg -i package.deb 安装/更新一个 deb 包 
	dpkg -r package_name 从系统删除一个 deb 包 
	dpkg -l 显示系统中所有已经安装的 deb 包 
	dpkg -l | grep httpd 显示所有名称中包含 "httpd" 字样的deb包 
	dpkg -s package_name 获得已经安装在系统中一个特殊包的信息 
	dpkg -L package_name 显示系统中已经安装的一个deb包所提供的文件列表 
	dpkg --contents package.deb 显示尚未安装的一个包所提供的文件列表 
	dpkg -S /bin/ping 确认所给的文件由哪个deb包提供 



## APT 软件工具 (Debian, Ubuntu 以及类似系统) 
	apt-get install package_name 安装/更新一个 deb 包 
	apt-cdrom install package_name 从光盘安装/更新一个 deb 包 
	apt-get update 升级列表中的软件包 
	apt-get upgrade 升级所有已安装的软件 
	apt-get remove package_name 从系统删除一个deb包 
	apt-get check 确认依赖的软件仓库正确 
	apt-get clean 从下载的软件包中清理缓存 
	apt-cache search searched-package 返回包含所要搜索字符串的软件包名称 



## 查看文件内容 
	cat file1 从第一个字节开始正向查看文件的内容 
	tac file1 从最后一行开始反向查看一个文件的内容 
	more file1 查看一个长文件的内容 
	less file1 类似于 'more' 命令，但是它允许在文件中和正向操作一样的反向操作 
	head -2 file1 查看一个文件的前两行 
	tail -2 file1 查看一个文件的最后两行 
	tail -f /var/log/messages 实时查看被添加到一个文件中的内容 



## 文本处理 
	cat file1 file2 ... | command <> file1_in.txt_or_file1_out.txt general syntax for text manipulation using PIPE, STDIN and STDOUT 
	cat file1 | command( sed, grep, awk, grep, etc...) > result.txt 合并一个文件的详细说明文本，并将简介写入一个新文件中 
	cat file1 | command( sed, grep, awk, grep, etc...) >> result.txt 合并一个文件的详细说明文本，并将简介写入一个已有的文件中 
	grep Aug /var/log/messages 在文件 '/var/log/messages'中查找关键词"Aug" 
	grep ^Aug /var/log/messages 在文件 '/var/log/messages'中查找以"Aug"开始的词汇 
	grep [0-9] /var/log/messages 选择 '/var/log/messages' 文件中所有包含数字的行 
	grep Aug -R /var/log/* 在目录 '/var/log' 及随后的目录中搜索字符串"Aug" 
	sed 's/stringa1/stringa2/g' example.txt 将example.txt文件中的 "string1" 替换成 "string2" 
	sed '/^$/d' example.txt 从example.txt文件中删除所有空白行 
	sed '/ *#/d; /^$/d' example.txt 从example.txt文件中删除所有注释和空白行 
	echo 'esempio' | tr '[:lower:]' '[:upper:]' 合并上下单元格内容 
	sed -e '1d' result.txt 从文件example.txt 中排除第一行 
	sed -n '/stringa1/p' 查看只包含词汇 "string1"的行 
	sed -e 's/ *$//' example.txt 删除每一行最后的空白字符 
	sed -e 's/stringa1//g' example.txt 从文档中只删除词汇 "string1" 并保留剩余全部 
	sed -n '1,5p;5q' example.txt 查看从第一行到第5行内容 
	sed -n '5p;5q' example.txt 查看第5行 
	sed -e 's/00*/0/g' example.txt 用单个零替换多个零 
	cat -n file1 标示文件的行数 
	cat example.txt | awk 'NR%2==1' 删除example.txt文件中的所有偶数行 
	echo a b c | awk '{print $1}' 查看一行第一栏 
	echo a b c | awk '{print $1,$3}' 查看一行的第一和第三栏 
	paste file1 file2 合并两个文件或两栏的内容 
	paste -d '+' file1 file2 合并两个文件或两栏的内容，中间用"+"区分 
	sort file1 file2 排序两个文件的内容 
	sort file1 file2 | uniq 取出两个文件的并集(重复的行只保留一份) 
	sort file1 file2 | uniq -u 删除交集，留下其他的行 
	sort file1 file2 | uniq -d 取出两个文件的交集(只留下同时存在于两个文件中的文件) 
	comm -1 file1 file2 比较两个文件的内容只删除 'file1' 所包含的内容 
	comm -2 file1 file2 比较两个文件的内容只删除 'file2' 所包含的内容 
	comm -3 file1 file2 比较两个文件的内容只删除两个文件共有的部分 




## 字符设置和文件格式转换 
	dos2unix filedos.txt fileunix.txt 将一个文本文件的格式从MSDOS转换成UNIX 
	unix2dos fileunix.txt filedos.txt 将一个文本文件的格式从UNIX转换成MSDOS 
	recode ..HTML < page.txt > page.html 将一个文本文件转换成html 
	recode -l | more 显示所有允许的转换格式 



## 文件系统分析 
	badblocks -v /dev/hda1 检查磁盘hda1上的坏磁块 
	fsck /dev/hda1 修复/检查hda1磁盘上linux文件系统的完整性 
	fsck.ext2 /dev/hda1 修复/检查hda1磁盘上ext2文件系统的完整性 
	e2fsck /dev/hda1 修复/检查hda1磁盘上ext2文件系统的完整性 
	e2fsck -j /dev/hda1 修复/检查hda1磁盘上ext3文件系统的完整性 
	fsck.ext3 /dev/hda1 修复/检查hda1磁盘上ext3文件系统的完整性 
	fsck.vfat /dev/hda1 修复/检查hda1磁盘上fat文件系统的完整性 
	fsck.msdos /dev/hda1 修复/检查hda1磁盘上dos文件系统的完整性 
	dosfsck /dev/hda1 修复/检查hda1磁盘上dos文件系统的完整性 



## 初始化一个文件系统 
	mkfs /dev/hda1 在hda1分区创建一个文件系统 
	mke2fs /dev/hda1 在hda1分区创建一个linux ext2的文件系统 
	mke2fs -j /dev/hda1 在hda1分区创建一个linux ext3(日志型)的文件系统 
	mkfs -t vfat 32 -F /dev/hda1 创建一个 FAT32 文件系统 
	fdformat -n /dev/fd0 格式化一个软盘 
	mkswap /dev/hda3 创建一个swap文件系统 



## SWAP文件系统 
	mkswap /dev/hda3 创建一个swap文件系统 
	swapon /dev/hda3 启用一个新的swap文件系统 
	swapon /dev/hda2 /dev/hdb3 启用两个swap分区 



## 备份 
	dump -0aj -f /tmp/home0.bak /home 制作一个 '/home' 目录的完整备份 
	dump -1aj -f /tmp/home0.bak /home 制作一个 '/home' 目录的交互式备份 
	restore -if /tmp/home0.bak 还原一个交互式备份 
	rsync -rogpav --delete /home /tmp 同步两边的目录 
	rsync -rogpav -e ssh --delete /home ip_address:/tmp 通过SSH通道rsync 
	rsync -az -e ssh --delete ip_addr:/home/public /home/local 通过ssh和压缩将一个远程目录同步到本地目录 
	rsync -az -e ssh --delete /home/local ip_addr:/home/public 通过ssh和压缩将本地目录同步到远程目录 
	dd bs=1M if=/dev/hda | gzip | ssh user@ip_addr 'dd of=hda.gz' 通过ssh在远程主机上执行一次备份本地磁盘的操作 
	dd if=/dev/sda of=/tmp/file1 备份磁盘内容到一个文件 
	tar -Puf backup.tar /home/user 执行一次对 '/home/user' 目录的交互式备份操作 
	( cd /tmp/local/ && tar c . ) | ssh -C user@ip_addr 'cd /home/share/ && tar x -p' 通过ssh在远程目录中复制一个目录内容 
	( tar c /home ) | ssh -C user@ip_addr 'cd /home/backup-home && tar x -p' 通过ssh在远程目录中复制一个本地目录 
	tar cf - . | (cd /tmp/backup ; tar xf - ) 本地将一个目录复制到另一个地方，保留原有权限及链接 
	find /home/user1 -name '*.txt' | xargs cp -av --target-directory=/home/backup/ --parents 从一个目录查找并复制所有以 '.txt' 结尾的文件到另一个目录 
	find /var/log -name '*.log' | tar cv --files-from=- | bzip2 > log.tar.bz2 查找所有以 '.log' 结尾的文件并做成一个bzip包 
	dd if=/dev/hda of=/dev/fd0 bs=512 count=1 做一个将 MBR (Master Boot Record)内容复制到软盘的动作 
	dd if=/dev/fd0 of=/dev/hda bs=512 count=1 从已经保存到软盘的备份中恢复MBR内容 



## 光盘 
	cdrecord -v gracetime=2 dev=/dev/cdrom -eject blank=fast -force 清空一个可复写的光盘内容 
	mkisofs /dev/cdrom > cd.iso 在磁盘上创建一个光盘的iso镜像文件 
	mkisofs /dev/cdrom | gzip > cd_iso.gz 在磁盘上创建一个压缩了的光盘iso镜像文件 
	mkisofs -J -allow-leading-dots -R -V "Label CD" -iso-level 4 -o ./cd.iso data_cd 创建一个目录的iso镜像文件 
	cdrecord -v dev=/dev/cdrom cd.iso 刻录一个ISO镜像文件 
	gzip -dc cd_iso.gz | cdrecord dev=/dev/cdrom - 刻录一个压缩了的ISO镜像文件 
	mount -o loop cd.iso /mnt/iso 挂载一个ISO镜像文件 
	cd-paranoia -B 从一个CD光盘转录音轨到 wav 文件中 
	cd-paranoia -- "-3" 从一个CD光盘转录音轨到 wav 文件中（参数-3） 
	cdrecord --scanbus 扫描总线以识别scsi通道 
	dd if=/dev/hdc | md5sum 校验一个设备的md5sum编码，例如一张 CD 



## 网络 - （以太网和WIFI无线） 
	ifconfig eth0 显示一个以太网卡的配置 
	ifup eth0 启用一个 'eth0' 网络设备 
	ifdown eth0 禁用一个 'eth0' 网络设备 
	ifconfig eth0 192.168.1.1 netmask 255.255.255.0 控制IP地址 
	ifconfig eth0 promisc 设置 'eth0' 成混杂模式以嗅探数据包 (sniffing) 
	dhclient eth0 以dhcp模式启用 'eth0' 
	route -n show routing table 
	route add -net 0/0 gw IP_Gateway configura default gateway 
	route add -net 192.168.0.0 netmask 255.255.0.0 gw 192.168.1.1 configure static route to reach network '192.168.0.0/16' 
	route del 0/0 gw IP_gateway remove static route 
	echo "1" > /proc/sys/net/ipv4/ip_forward activate ip routing 
	hostname show hostname of system 
	host www.example.com lookup hostname to resolve name to ip address and viceversa(1) 
	nslookup www.example.com lookup hostname to resolve name to ip address and viceversa(2) 
	ip link show show link status of all interfaces 
	mii-tool eth0 show link status of 'eth0' 
	ethtool eth0 show statistics of network card 'eth0' 
	netstat -tup show all active network connections and their PID 
	netstat -tupl show all network services listening on the system and their PID 
	tcpdump tcp port 80 show all HTTP traffic 
	iwlist scan show wireless networks 
	iwconfig eth1 show configuration of a wireless network card 
	hostname show hostname 
	host www.example.com lookup hostname to resolve name to ip address and viceversa 
	nslookup www.example.com lookup hostname to resolve name to ip address and viceversa 
	whois www.example.com lookup on Whois database 
